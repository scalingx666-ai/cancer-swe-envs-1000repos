# Issue

**Title:** Updates related to bam index and the implementation of a WDL that takes coverage as input

## Description

- Updated the check for the existences of a bam index so that now it accepts csi in addition to bai (Issue #72).
- Added a workflow that takes coverage file as input instead of bam. It is useful when there is an upgrade in HMM-Flagger but the read alignments and bam2cov outputs are the same.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `48810876c13e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.