# Issue

**Title:** Integrate TM Docker plug-in changes to enable passing UID:GID as argu…

## Description

Updates MONAI Deploy Express:


- Integrates TM  to enable passing `UID:GID` as argument.
- add new liver tumor 2.0 sample

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2cbaefd0bfdb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.