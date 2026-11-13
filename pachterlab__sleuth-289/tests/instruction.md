# Issue

**Title:** Only pass data.table objects to data.table::melt and data.table::recast

## Description

Passing data frames to data.table reshaping functions is deprecated, so precast these objects to data.table before calling data.table::melt and data.table::recast.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `20e493fb98cb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.