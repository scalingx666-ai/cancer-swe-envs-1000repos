# Issue

**Title:** Allow user to supply pre-loaded RefCDS-style object instead of file path

## Description

If users have their own RefCDS objects, it's often useful to be able to supply them directly rather than via a file path.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c9fa29abf9c4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.