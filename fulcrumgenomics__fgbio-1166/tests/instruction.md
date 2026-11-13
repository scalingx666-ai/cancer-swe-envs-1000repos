# Issue

**Title:** fix(umi): make consensus read downsampling deterministic

## Description

## Problem

When a cap is set (`--max-reads`, `--max-reads-per-strand`, `--max-read-pairs`) and a tag family exceeds it, consensus output was not reproducible under `--threads > 1`. The same input BAM produced different consensus bases, qualities and depths on every run.

The downsampler used a `Random(42)` held on the caller instance:

```scala
private val random = new Random(42)
...
val capped = if (reads.size <= this.options.maxReads) reads else this.random.shuffle(reads).take(this.options.maxReads)
```

The RNG is stateful, so which reads survive depends on how many families that instance already downsampled. `ConsensusCallingIterator` gives each thread its own caller via `emptyClone()`, and `ParIterator` hands chunks to a fork-join pool, so the family-to-thread assignment — and hence each caller's RNG position for a given family — varies run to run.

This affects `CallMolecularConsensusReads`, `CallDuplexConsensusReads` and `CallCodecConsensusReads`, all of which downsample through `VanillaUmiConsensusCaller.consensusCall`. Single-threaded runs were already deterministic.

## Fix

Rank reads by a Murmur3 hash of their read name and keep the lowest-ranking ones. The retained subset becomes a pure function of the family, independent of the caller's history, the thread count, and the order reads arrive in. This mirrors the existing hash-based downsampling in `CollectDuplexSeqMetrics` and `SamOrder.Random`.

The rank is computed once per read rather than passed to `sortBy`, which re-evaluates its key on every comparison (measured at ~25-30x the element count for large families, each evaluation hashing a read name and allocating an `Option`).

## Behaviour changes

Two things change for anyone who sets a cap. Both are intentional and want a release note.

1. **Which reads are retained differs from 4.1.0**, single-threaded runs included. There is no way to fix the determinism bug while preserving the old selection, since the old selection was the bug.
2. **Both ends of a template are now retained or discarded together.** Ends are downsampled by separate `consensusCall` invocations; under the old independent shuffles each end sampled templates independently, whereas mates share a read name and so now share a rank. This makes `--max-read-pairs` actually cap read pairs. It is pinned by a test and stated in the arg docs.

## Tests

Four new tests, each watched failing before the implementation existed:

- the subset a caller picks does not depend on how many families it already downsampled — the original bug;
- `CallDuplexConsensusReads` produces byte-identical output at `--threads 1` and `--threads 8` over 300 molecules (spanning several `ConsensusCallingIterator` chunks rather than relying on fork-join splitting within one);
- the subset is invariant to input read order;
- both ends of a template are retained together.

Plus a golden test pinning *which* reads are retained, whose expected value was derived independently from htsjdk's `Murmur3(42)` rather than from fgbio. Without it, a deterministic-but-biased rule (e.g. sorting by read name, which on Illumina names sorts by tile/x/y) passes every test above.

Full suite: 1611 tests, 0 failures.

## Second commit

`CallDuplexConsensusReads` accepted `--max-reads-per-strand 0`, which emptied every strand and then failed deep in consensus calling with a bare `IllegalArgumentException: requirement failed: Too few reads to create a consensus.` The sibling tools already validate their equivalent options. Separate commit; reviewable independently.

## Known gap, deliberately not addressed here

Reads dropped by downsampling are not routed through `rejectRecords`: they are counted as used in `raw_reads_used` / `frac_raw_reads_used` and never reach `--rejects`. A family of 10 capped to 3 reports `raw_reads_used = 10` while the consensus carries `cD:i:3`. This is pre-existing — the old `shuffle.take` lost them the same way — and fixing it means a new `RejectionReason`, touching the `usedByVanilla`/`usedByDuplex`/`usedByCodec` tables and metrics output. It does not belong in a determinism fix, and is tracked separately in #1167.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `798aca4a48b7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.