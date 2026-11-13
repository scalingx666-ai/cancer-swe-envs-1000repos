# Issue

**Title:** only merge read selection passes when both enabled

## Description

Fixes a segmentation fault when 1-pass read selection is skipped but 2-pass read selection is not.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2c435005726c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.