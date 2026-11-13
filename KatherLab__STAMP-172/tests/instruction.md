# Issue

**Title:** Fix/dropna inconsistency

## Description

`drop_patients_with_missing_ground_truth` is now a config option with default true on the tasks that use that loading behavior

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d5f34376ec67`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.