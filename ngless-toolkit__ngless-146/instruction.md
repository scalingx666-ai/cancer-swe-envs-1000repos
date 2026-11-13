# Issue

**Title:** Build static Linux image with GitHub Actions

## Description

We have been using GitLab CI to build these static binaries but that process has been failing for a while.
Discontinuing it in favor of a single build process using GitHub Actions.

The result can be previewed [here](https://github.com/unode/ngless/actions/runs/953412662).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8fa9b0018e56`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.