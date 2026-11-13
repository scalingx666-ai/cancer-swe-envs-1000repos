# Issue

**Title:** Create the "models" directory if not found.

## Description

The 'models' directory is not committed to the repository (another solution).

At least with my python 3.6 environment, the shutil.copy() failed because ./models didn't exist. This is the moral equivalent of a ```mkdir -p models```.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d1f3433a6baf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.