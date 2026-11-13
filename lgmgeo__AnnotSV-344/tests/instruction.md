# Issue

**Title:** Adding shellcheck pipeline

## Description

-> add automatic pipeline for bash scripts, fails on error but still shows warnings
-> fixed "bugs" to allows the merge

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2e80f00620d6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.