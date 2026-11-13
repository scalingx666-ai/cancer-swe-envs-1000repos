# Issue

**Title:** bug fix: use reshape2::melt instead of stats::reshape

## Description

stats::reshape would munge values (typically gene names)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1ebad2f3dca9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.