# Issue

**Title:** Fix strelka

## Description

Somehow the conda install of strelka recently broke (without a version change). This fix switches the Dockerfile to downloading and installing the strelka binary release directly, rather than using conda.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `95e36af421d2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.