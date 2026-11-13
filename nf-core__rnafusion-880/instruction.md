# Issue

**Title:** Bump version to 4.2.1dev

## Description

Post-release version bump after the `4.2.0` release (https://github.com/nf-core/rnafusion/releases/tag/4.2.0).

- `nf-core pipelines bump-version 4.2.1dev` (`nextflow.config`, `.nf-core.yml`, `assets/multiqc_config.yml`, `ro-crate-metadata.json`)
- New empty `v4.2.1dev - [unreleased]` section in `CHANGELOG.md`

## PR checklist

- [x] This comment contains a description of changes (with reason).
- [x] Make sure your code lints (`nf-core pipelines lint`).
- [x] `CHANGELOG.md` is updated.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7fd6cc7d808a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.