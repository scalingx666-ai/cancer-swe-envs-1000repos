# Issue

**Title:** Set v4.2.0 release date, update starfusion/detect

## Description

Prepares `dev` for today's 4.2.0 release.

- Sets the `v4.2.0` release date in `CHANGELOG.md` (2026-11-12).
- Pulls in nf-core/modules#13701, which adds an nf-test for `STARFUSION_DETECT` with a chimeric junction file as input (#593). Only the module's test files change, so pipeline behaviour and snapshots are unaffected, and `nf-core pipelines lint` won't flag the module as outdated.

## PR checklist

- [x] `CHANGELOG.md` is updated.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b183cd60e162`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.