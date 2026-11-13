# Issue

**Title:** split tests to allow for testing without spades installed

## Description

- Allow for testing without spades installed
- Switch from nose->pytest since the former is deprecated

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3e223bee8ae5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.