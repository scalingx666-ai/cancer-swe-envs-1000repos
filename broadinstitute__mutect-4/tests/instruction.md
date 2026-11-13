# Issue

**Title:** Removing benchmarking related files

## Description

I removed SomaticSpike and LibraryReadFilter.  These have moved to somatic-benchmark for the time being.
LibraryReadFilter will be transitioned into the gatk core.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0d8dfd9b6caa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.