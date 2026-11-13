# Issue

**Title:** Fix ModuleNotFoundError for some scripts in supply/

## Description

by removing the `version.__version__` import. The `version.__version__` variable is not used anywhere in these scripts, anyways.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ac0578ecaa09`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.