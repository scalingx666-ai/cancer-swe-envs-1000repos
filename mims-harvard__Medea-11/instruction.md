# Issue

**Title:** docs: fix package repository links

## Description

## Summary
- update package metadata links from the stale Medea-1.0 URL to the current mims-harvard/Medea repository
- keep setup.py and pyproject.toml consistent

## Validation
- python -m compileall medea main.py utils.py
- python -c "import pathlib; text=pathlib.Path('pyproject.toml').read_text(encoding='utf-8'); assert 'Medea-1.0' not in text; assert 'https://github.com/mims-harvard/Medea' in text; print('metadata links ok')"
- git diff --check

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d44d1d49928a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.