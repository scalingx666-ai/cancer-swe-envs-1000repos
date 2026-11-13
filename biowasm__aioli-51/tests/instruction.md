# Issue

**Title:** Add a function "downloadBlob" for zip downloading multiple files and solve multiple space problem in the command arguments

## Description

I made two modifications:

1. Add a function called "downloadBlob" so I can use jszip to zip multiple files for downloading.
2. Trim spaces and split by `/ +/` to avoid space problems for commands for `CLI.exec`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b132f5a6cca2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.