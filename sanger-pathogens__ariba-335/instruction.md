# Issue

**Title:** Require pysam>=0.21.0; fix mpileup call

## Description

Update to pysam 0.21.0, and fix the bcftools/mpileup call.

The VCF of this updated mpileup has _slightly_ different values (read counts/depths etc changed a tiny bit), but not enough to worry about. Tests/test files updated accordingly.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a065b3891226`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.