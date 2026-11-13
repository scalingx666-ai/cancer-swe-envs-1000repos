# Issue

**Title:** Single pileup pass per chromosome with improved base indexing accuracy

## Description

Changes in this script consolidate pileup calls to once per chromosome instead of once per position, correct base indexing, and move VCF quality filtering earlier to skip low-quality positions before pileup.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2b55d94fca70`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.