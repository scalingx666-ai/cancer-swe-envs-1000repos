# Issue

**Title:** refactor: use selective imports from BiocGenerics

## Description

- Move ProtGenerics and BiocGenerics from Depends to Imports
- Use selective imports from BiocGenerics.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a69e0cb891a6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.