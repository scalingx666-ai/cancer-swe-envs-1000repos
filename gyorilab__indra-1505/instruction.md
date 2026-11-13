# Issue

**Title:** Update Docker build

## Description

This PR does some minor cleanup on the Docker build as a . Specifically
- Change ADD to COPY
- Consolidate apt installs and avoid putting apt and pip cache into image
- Remove some unnecessary/outdated explicit installs
- Update deprecated ENV usage

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `08646c18c5ea`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.