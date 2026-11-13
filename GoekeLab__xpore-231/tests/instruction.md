# Issue

**Title:** Repackage xpore & add Yuk Kei's CI

## Description

Basically what it says on the tin, modernizes the packaging as `setup.py` is considered deprecated now.
Also took the opportunity to clean up some parts of the code and update some depenencies (eg numpy, pandas to version 2) and add the CI Yuk Kei had in the upstream dev branch.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4880e65716aa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.