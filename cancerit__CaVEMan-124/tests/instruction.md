# Issue

**Title:** fix index crash due to bad chr_name malloc (and other things as I went)

## Description

split.c is where the bugs were.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c357a9ad58f1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.