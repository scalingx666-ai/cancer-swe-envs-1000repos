# Issue

**Title:** expand environment variables in paths

## Description

when running MuPeXI in different (remote) environments, users don't always know the exact path of the executables and biological data.
allowing for environment variables in the paths makes it possible to use the same `config.ini` for all environments.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1ea0805a651c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.