# Issue

**Title:** Add -F 2308 for samtools view

## Description

Filter SEQ with value "*" by filtering unmapped reads, secondary reads
and supplementary reads

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f513449ed9eb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.