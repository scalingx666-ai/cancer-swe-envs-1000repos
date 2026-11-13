# Issue

**Title:** MAINT: address internal deprecation warnings

## Description

## Summary by Sourcery

Remove internal deprecation-warning sources by using metadata consistently and making cleanup safe for partially initialized objects.

Bug Fixes:
- Prevent object finalizers from raising errors when construction fails before annotation database initialization.

Enhancements:
- Replace alignment and sequence collection test usage of the deprecated `info` attribute with `metadata`.
- Update related tests and naming to reflect metadata-based object state and preserve existing metadata behavior across transformations, serialization, and parsing.

Tests:
- Add coverage ensuring failed construction cleanup is silent and unraisable-exception warnings are treated as errors.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2be49bc0f49a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.