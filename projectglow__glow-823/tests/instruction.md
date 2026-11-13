# Issue

**Title:** Fix GFF reader failing under ANSI mode (Spark 4 default)

## Description

## What changes are proposed in this pull request?

On Spark 4, `spark.read.format("gff").load(...)` fails for basically any GFF3 file:

```
[CAST_INVALID_INPUT] The value 'RefSeq' of the type "STRING" cannot be cast to "DOUBLE" because it is malformed. ... SQLSTATE: 22018
```

`GffDataSource.filterFastaLines` drops FASTA lines with `!isnull(coalesce(source, type, start, end, score, strand, phase, attributes))`. `coalesce` needs a common type for its arguments. Under ANSI type coercion, STRING and DOUBLE (the `score` column) widen to DOUBLE, so the analyzer wraps every string column in a cast:

```
Filter NOT isnull(coalesce(cast(source as double), cast(type as double), cast(start as double), cast(end as double), score, cast(strand as double), cast(phase as double), cast(attributes as double)))
```

The first non-numeric `source` value then throws. Spark 4 enables `spark.sql.ansi.enabled` by default, so the GFF reader was broken out of the box on `glow-spark4`. Spark 3.5 with ANSI enabled is affected as well; the code itself has not changed since 2024.

This PR replaces the `coalesce` with an OR of `isNotNull` checks. It keeps the same meaning ("some column other than `seqId` is non-null") and involves no type coercion.

CI didn't catch this because `GlowBaseTest` turns ANSI off for the whole suite (). The new test turns ANSI on explicitly for its own scope. #808's audit covered Catalyst expressions; this was DataFrame-level implicit coercion. I grepped the rest of the codebase for `coalesce`/`greatest`/`least` and found no other mixed-type uses.

## How is this patch tested?
- [x] Unit tests

- New `GffReaderSuite` test, "Read gff with ANSI mode enabled". It reads `test_gff_with_fasta.gff` with `spark.sql.ansi.enabled=true` and checks the row count, `df.count == df.rdd.count`, and a filter on `source`.
  - Without the fix it fails with the `CAST_INVALID_INPUT 'RefSeq'` error above on both Spark 4.1.0 and Spark 3.5.1.
  - With the fix, the full `GffReaderSuite` (17 tests) passes on Spark 4.1.0 and Spark 3.5.1.
- Full `core/test` on Spark 4.1.0: 778 passed, 0 failed.
- `scalafmtCheck` passes.
- I reproduced the original report locally on PySpark 4.1.0 with the NCBI GRCh38.p14 RefSeq GFF (`GCF_000001405.40_GRCh38.p14_genomic.gff.gz`).

This pull request and its description were written by Isaac.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0539c76b95c7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.