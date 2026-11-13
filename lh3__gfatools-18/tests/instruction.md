# Issue

**Title:** Fix SQL glitches in INSERT INTO {seg,arg} when rank is 0

## Description

This fixes two glitches in the SQL generation.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `76c4d42b874b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.