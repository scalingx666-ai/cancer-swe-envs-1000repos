# Issue

**Title:** [query] Fix use-after-free of lazy inner elements in StreamFlatMap

## Description

Fixes a use-after-free in `StreamFlatMap` when its inner stream requires per-element memory management and the inner element is computed lazily.

```diff
 StreamFlatMap.LproduceElement
   if first
     ...start the first inner stream...
+  else
+    innerRegion.clearRegion()          // clear just before the next inner pull
   pull inner
   result.track(innerRegion)
   result.track(outerRegion)
-  innerRegion.clearRegion()            // used to clear right after producing
   goto LproduceElementDone             // consumer evaluates innerProducer.element here
```

Stream elements are lazy. A `StreamMap` element is its body, run against the child's element region when the consumer reads it. Before this change, a body that allocates (e.g. `ToArray`) wrote into the fresh memory that `clearRegion` had just swapped in. `resultElementRegion` held no reference to that memory.

- **Most elements:** the next pull tracked the inner region before clearing it, which kept the memory alive by accident.
- **Last element of each inner stream:** the next pull ended the inner stream, and the inner region was freed while the consumer still held the element.

`StreamZipJoin` holds each input's current element while it pulls the other inputs, so it reads that freed memory.

How users hit it:

```text
read_matrix_table(path, _intervals=ivs)    // requested ∩ on-disk partitioner != requested
  AbstractRVDSpec.readZippedLowered
    TableStage.repartitionNoShuffle         // fast path: every partition is a StreamFlatMap
annotate_entries(...)                       // optimizer pushes this StreamMap into the flatMap body
_localize_entries(...)
Table.multi_way_zip_join([...])             // StreamZipJoin holds the last row of an interval across a pull
```

The last row of each read interval gets a garbage `__entries` array. Seen in practice as:
- wrong results
- `length mismatch between entry array and column array`
- part files that don't decode
- SIGSEGVs in generated code

This came up in a VDS combiner merge.

The bug dates from d07b2e9853 ([query] Fix memory management in new stream emitter, #10299), which added the track-then-clear scheme. `StreamGrouped`'s inner producer has the same pattern. It only goes wrong if a consumer holds a group's last element across a pull, which nothing is known to do, so this PR leaves it alone.

## Evidence

- **Before:** `EmitStreamSuite.testStreamFlatMapLazyInnerElementOutlivesInnerStream` fails with an assertion error.
  **After:** it passes.

  ```text
  input = flatMap(ToStream([[0,1,2],[3,4,5]], true)) { part =>
            map(takeWhile(map(ToStream(part, true))(k => {k, a: [k*100 + j for j < 5]}))(true)) { row =>
              {k: row.k, a: [x + 0 for x in row.a]} } }       // lazily built array
  zipJoin([input, input], "k")
  assert every row's `a` arrays == [k*100 + j for j < 5]      // key 2 read freed memory before
  ```

- **Before:** `test_multi_way_zip_join_of_repartitioned_matrix_reads` fails (2/2 runs).
  **After:** it passes (2/2 runs).

  ```text
  3 matrix tables, 1000 rows x 5 cols, same on-disk partitioning
  read each with _intervals (one interval runs past the data), annotate_entries, _localize_entries
  multi_way_zip_join
  assert every defined input has len(__entries) == 5
  ```

  Before:

  ```text
  E       assert [Locus(contig=chr1, position=1851, ...)] == []
  ```

- Standalone repro (K=3, 1000x5), before and after:

  ```text
  before: rows 237; rows with wrong entry count 1
            BAD Struct(locus=chr1:1851, lens=[5, 5, -65433604])
  after:  rows 237; rows with wrong entry count 0
  ```

  It also passes at 40000x100 with K=2 and K=3, which failed before.

- `EmitStreamSuite` (39 tests, including the flatMap memory-scaling tests), `IRSuite`, `TableIRSuite`, `MatrixIRSuite` and `OrderingSuite` all pass.

## Merge Danger

**Door:** two-way

A codegen-only change in one stream node. No serialized formats, IR, or APIs change. Reverting the commit restores the old behavior exactly.

**Blast Radius:** broad

Every `StreamFlatMap` whose inner stream requires per-element memory management now clears its inner region at the next pull rather than right after producing. That covers many lowered pipelines: table and matrix reads that repartition, and any flatMap over per-element-managed streams. The inner region now holds the current element's memory until the next pull. It is still cleared once per element, so peak memory per element is unchanged (the existing memory-scaling tests cover this). A mistake here would show up as memory growth or wrong results in flatMap-heavy pipelines, not as compile errors.

---
No batch security implications

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8bf49a42f23c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.