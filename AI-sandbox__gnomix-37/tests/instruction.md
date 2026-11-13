# Issue

**Title:** Modifying train pipeline to be more memory efficient

## Description

- Save gen0 for all splits - train1, train2 and val
- Force train1 split's generations to be [0]
- Add Gnomix.retrain_base() as a separate function

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `aeaee39abdbd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.