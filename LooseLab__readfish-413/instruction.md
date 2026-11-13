# Issue

**Title:** Catching pause state

## Description

Since an update to the minKNOW API we have seen the addition of a pause state. If a user actively pauses the flowcell, readfish may disconnect without the user expecting this. This adds the acceptable pause states (if they exist) and prevents readfish from terminating at a pause.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c6e52c7e8471`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.