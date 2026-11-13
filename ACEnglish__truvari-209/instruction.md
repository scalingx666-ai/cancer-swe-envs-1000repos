# Issue

**Title:** Allow csi-indexed vcf files

## Description

It looks like truvari already works with csi-indexed VCF files via support from pysam, but just needs updated input validation.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a8dbd3066f75`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.