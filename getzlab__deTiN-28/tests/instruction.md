# Issue

**Title:** Fix bug in cluster_segments found while testing on CPTAC data.  This …

## Description

…problem appeared when the number of segments was less than 3.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3b0b9598894d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.