# Issue

**Title:** Update mkdirs

## Description

makedirs() creates all the intermediate directories if they don't exist.
mkdir() can create a single sub-directory, and will throw an exception if intermediate directories that don't exist are specified.
The current implementation with mkdir will not work if the intermediate data folder does not exist.
Alternatively, the makedirs() will generate intermediate folders if needed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `84a02e9e9ddf`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.