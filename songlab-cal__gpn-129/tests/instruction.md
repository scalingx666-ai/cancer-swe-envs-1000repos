# Issue

**Title:** Reduce Dependabot updates to quarterly

## Description

## Summary

Reduce routine dependency-maintenance noise by changing Dependabot checks from weekly to quarterly for uv, pre-commit, and GitHub Actions. Limit open version-update PRs to one per ecosystem while retaining the existing minor/patch groups and major-version exclusions.

## Verification

- `git diff --check` passed.
- `uv run pre-commit run --all-files` passed, including YAML validation.
- Confirmed the diff contains only the three schedule changes and three PR limits. Full tests and documentation build are not required for this configuration-only change.

## Review checklist

- [x] The change stays within the maintained scope in `AGENTS.md`.
- [x] Tests, documentation, and dependency metadata are updated together where applicable; this change only adjusts Dependabot scheduling and limits.
- [x] Normal tests remain offline; no model, dataset, or MSA is downloaded in CI.
- [x] No scientific output or public API changes; fixture review and changelog entries are not applicable.
- [x] No secret, private asset, or institutional filesystem path is committed.
- [x] No releases, tags, repository settings, PyPI, or Hub writes are proposed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6f28c81bcbfe`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.