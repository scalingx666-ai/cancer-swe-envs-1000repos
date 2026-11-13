# Issue

**Title:** using MacOS-compatible CPU count

## Description

This PR addresses an issue that MacOS systems do not have `os.sched_getaffinity` (see ) Thank @inspirewind for reporting this in #122 !

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e8045fec593b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.