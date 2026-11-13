# Issue

**Title:** Fixes failure due to CPLEX not connected with gGnome and Sequenza installation.

## Description

**Description:**

- Updated README.md, DESCRIPTION paths, gGnome CPLEX issue, Sequenza installation.
- JaBbA was breaking due to no CPLEX with gGnome, so it was necessary.

**Changes:**

- JaBbA will check if gGnome has CPLEX connected, otherwise it will try to reinstall gGnome to add CPLEX.
- Sequenza was removed from CRAN, so updated the archive path to address dependency installation issue.
- Updated DESCRIPTION paths to match correct paths for dependency packages.
- Updated version to V1.1 in DESCRIPTION to match current release.

**Impact:**

- This should address the fix for JaBbA failure due to gGnome without CPLEX and fix sequenza installation.

**Related Issues:**

-  .

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `277f4c087b7e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.