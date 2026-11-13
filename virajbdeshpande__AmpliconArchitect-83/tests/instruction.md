# Issue

**Title:** patch for MD tag bugfix, docker updates & update shebang to use env python

## Description

shebang update makes AA/PAA more compatible when used inside conda environments.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c4acf0a9a420`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.