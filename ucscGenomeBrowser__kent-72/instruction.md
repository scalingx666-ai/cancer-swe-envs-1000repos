# Issue

**Title:** Set locale explicitly to English

## Description

Output of commands may differ if you have different locale settings. Therefore searching for certain strings might fail.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5371d68730bd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.