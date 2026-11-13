# Issue

**Title:** trf411 longpath bufferoverfix

## Description

I implemented a trf 4.11 that supports fixing buffer overflow issues with long path names and applied @aglabx/TRF code for int_64 to support very large chromosome assemblies. This is linux64 compiled code - you may also want to provide stubs/links to git module checkouts of a repo for users.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f8b8aaa0e247`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.