# Issue

**Title:** genome_updater v0.10.0

## Description

- New option '-H copy' to enable use in filesystem without link support, with fixes and standardize use of links #116
- `history.tsv` is now used as a base to define current version label and is mandatory for fix/update #118

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5eafcb3ecad2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.