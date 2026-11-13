# Issue

**Title:** 290 speed up sparse random walk

## Description

Refactor the C code of the sparse and missing value random walks to score gene sets faster, by going only through the genes in the gene set and using a hybrid qsort/radix approach to sort gene set ranks that scales better with larger gene sets. Replaced previous memcpy/memset by Memcpy/Memzero calls.

This refactoring work has been developed with the assistance of Claude (Anthropic).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7186a8f1d696`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.