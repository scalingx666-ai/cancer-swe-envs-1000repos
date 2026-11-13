# Issue

**Title:** STRY0020817 - Manually update gene-drug key database

## Description

**Description**

StarAMR's gene-drug database is missing entries corresponding to IDs within the CGE Resfinder database. These are primarily variants of existing genes. We need to add this missing IDs to the gene-drug key to prevent unknown[...] from being reported.

**Acceptance Criteria**

- [x] Add corresponding entries for the missing phenicol FloR and phenicol CmlA.
- [x] Note the capitalization differences in gene IDs from previous entries. The newer entries in the CGE database have different capitalization than the old entries. We will probably need to match these differences correctly.
- [x] Test that the new and old floR/FloR and cmlA/CmlA are being handled correctly.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `be26591c1898`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.