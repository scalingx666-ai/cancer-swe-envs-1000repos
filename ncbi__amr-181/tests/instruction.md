# Issue

**Title:** Refactor and improve github action tests

## Description

- Factored out some common parts to "actions" (though more could be done here)
- Shifted from conda to micromamba for the bioconda tests
- Fixed a bug with uploading artifacts from jobs that compile from source
- Added optional tmate shells to assist with debugging

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4d10c01ad2aa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.