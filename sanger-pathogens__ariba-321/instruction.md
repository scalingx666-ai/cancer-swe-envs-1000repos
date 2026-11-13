# Issue

**Title:** Skip whole genome records

## Description

In order to prepare the NCBI acquired gene database, the records that are whole genome as determined by a prefix of 'AP' should be skipped

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5df88c85decd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.