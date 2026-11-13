# Issue

**Title:** Support gzipped barcode files

## Description

## Summary
- Read barcode lists with `gzip.open(..., rt)` when the file path ends in `.gz`.
- Normalize gzipped barcode lists into the existing temporary `.txt` barcode chunks so downstream scripts can keep using normal text files.
- Add regression coverage for counting and splitting gzipped barcode files.

.

## Validation
- `git diff --check`
- `git diff --cached --check`
- Not run locally: test suite

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ef4ea8b9f441`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.