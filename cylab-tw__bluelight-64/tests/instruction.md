# Issue

**Title:** fix: updated OAuth plugin to override the fetch header for token

## Description

- Updated OAuth plugin to override the fetch header for token, for the new wado loader that uses fetch.
- Fixed a bug where the URL Parameters is not removed completely due to using the wrong function (removeURLParameter -> removeURLParameters).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cbfe83cb8a14`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.