# Issue

**Title:** Bump to v0.5.0

## Description

# Change Log

### Changed

- Dropped python3.8 support
- Switched package manager `poetry` to `rye`

### Fixed

- Fixed consensus sequence extraction code to suppress biopython deprecated warning message

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b540ae7f4f5b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.