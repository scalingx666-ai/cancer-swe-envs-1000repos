# Issue

**Title:** Fix seed dedup: rev only the current x[0] group

## Description

Previous rev on whole array scrambles the sort, breaking dedup.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f0fd108456d4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.