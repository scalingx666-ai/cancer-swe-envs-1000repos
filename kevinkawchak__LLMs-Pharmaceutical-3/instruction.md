# Issue

**Title:** Add GitHub standards, CI pipeline, and restructure documentation (v4.…

## Description

…2.0)

- Add CI workflow with ruff lint-and-format across Python 3.10/3.11/3.12
- Add ruff.toml excluding Code/ research notebooks from lint checks
- Add CHANGELOG.md with version history v1.0.0 through v4.2.0
- Add CONTRIBUTING.md, CODE_OF_CONDUCT.md, SECURITY.md, SUPPORT.md
- Add CITATION.cff with Zenodo DOIs and .gitignore
- Add issue templates (bug report, feature request) and PR template
- Restructure main README with badges, manuscript table, research areas, timeline diagram, and prominent LLM Papers link
- Expand Code/README.md with directory index and file/notebook counts
- Expand R&D/README.md with full 70-document catalog by topic
- Add V4.2.0_RELEASE.md release notes

https://claude.ai/code/session_01MQ6HLt3idZE4fPdxnDBKLs

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c9c5129c5373`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.