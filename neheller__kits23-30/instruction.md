# Issue

**Title:** Fix surface distances package name

## Description

Please feel free to take over for the tasks in the checklist.

## Checklist

- [ ] Merged latest `master`
- [ ] Updated version number in `README.md`
- [ ] Added changes to `changelog.md`
- [ ] Updated version number in `setup.py`
- [ ] Version number in `kits23/_version.py` matches `setup.py`
- [ ] (only when updating dataset) Ran `annotation.import` to completion

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e2822085ffdd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.