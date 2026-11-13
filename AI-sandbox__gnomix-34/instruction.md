# Issue

**Title:** Base model updates

## Description

## Houskeeping for basemodels

Biggest updates are
- Equally sized windows by padding the last one
- Few unit tests for the base models
- Add typing
- Few dimension checks
- Remove time tracking
- import string kernels from https://pypi.org/project/string-kernels/
- skip base simulation as the default behavior.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `375d216b399f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.