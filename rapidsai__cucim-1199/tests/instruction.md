# Issue

**Title:** ci: Revert matrix_type overrides in for CUDA 13.4

## Description

Contributes to

CUDA 13.4 is now part of the default `pull-request` and `nightly` matrices in `shared-workflows`,
so the temporary `cuda-13-4-*` `matrix_type` overrides are no longer needed.

ref:

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3c5a363c3153`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.