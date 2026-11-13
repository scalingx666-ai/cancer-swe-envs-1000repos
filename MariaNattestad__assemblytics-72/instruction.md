# Issue

**Title:** Add pylint to CI; add PR preview deployments

## Description

## Summary

**Pylint:**
- Config in `pyproject.toml`: cosmetic/complexity checks disabled, `max-line-length=250`, fail-under=9.0 (currently scores 9.48/10)
- Fixed real issues in files touched this sprint: `bare-except` → `Exception`, `== True` → truthiness, undefined loop variable (`query` in uniq_anchor), unused numpy imports in `nchart.py` and `dotplot.py`
- Added `pylint` to `[dev]` extras and CI step in `test.yml`

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a509ddf93598`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.