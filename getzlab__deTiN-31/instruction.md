# Issue

**Title:** fix uninitialized variable bug when using only ssnvs

## Description

Fixing a bug that breaks deTiN when running with only SSNVs - `n_calls_pre` was not calculated when only SSNV data is passed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0f8fb0977a1c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.