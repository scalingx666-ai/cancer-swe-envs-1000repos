# Issue

**Title:** Bugfix. One could not specify CONPAIR_DIR on the command line.

## Description

Missing `opts` when referring to command line parameter `conpair_dir`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0cdebe30e1e4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.