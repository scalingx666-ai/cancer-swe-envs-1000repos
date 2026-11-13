# Issue

**Title:** Fix Quick Start runners for classification and imputation

## Description

## Summary
- Update classification and imputation shell runners so README Quick Start commands complete end-to-end.
- Patch GAIN and classical impute baselines used by those runners.
- Refresh README Quick Start guidance to match the fixed entry points.

## Test plan
- [ ] Run `scripts/run_classification.sh` from a clean checkout and confirm it finishes without path/env errors.
- [ ] Run `scripts/run_imputation.sh` (GAIN + classical) and confirm outputs land in the expected results paths.
- [ ] Spot-check README Quick Start commands against the updated scripts.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e88c5a4168a6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.