# Issue

**Title:** isdigit function is deprecated

## Description

The isdigit function in POSIX was removed as of v5.24. I've replaced with a simple check that should work instead. I haven't removed POSIX from getting loaded (line 8) because I'm not sure whether it's needed elsewhere.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b2841b2c0388`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.