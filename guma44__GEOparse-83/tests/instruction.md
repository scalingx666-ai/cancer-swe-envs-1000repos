# Issue

**Title:** Fix issue when GEO metadata contains commas

## Description

Hi there,

I found a bug when the GEO metadata contains "commas", which currently breaks the construction of the metadata data frame. Sharing this easy fix in case others find it useful.

Thanks for such a nice package!
Alex

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `10abe10cbb2c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.