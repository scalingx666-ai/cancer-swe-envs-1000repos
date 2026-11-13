# Issue

**Title:** fix: high cov pushed all likelihoods to 0

## Description

Downsamples qual scores to lists of 450 of less. 
This prevents an error where the likelihood of AA, BB, and AB get pushed to 0.0.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c59e9389a6d4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.