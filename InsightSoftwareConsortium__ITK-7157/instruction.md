# Issue

**Title:** BUG: Fail Azure Linux dependency install step on first error

## Description

Inspired by failure in #7153.

## PR Checklist
- [x] No [API changes](https://github.com/InsightSoftwareConsortium/ITK/blob/main/CONTRIBUTING.md#breaking-changes) were made (or the changes have been approved)
- [x] No [major design changes](https://github.com/InsightSoftwareConsortium/ITK/blob/main/CONTRIBUTING.md#design-changes) were made (or the changes have been approved)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7872171e7cea`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.