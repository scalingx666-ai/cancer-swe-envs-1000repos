# Issue

**Title:** Fix bug in create tensor

## Description

beginToEnd index changed to map the position to a list of tuples instead of a tuple to fix

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bc783f1ddc50`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.