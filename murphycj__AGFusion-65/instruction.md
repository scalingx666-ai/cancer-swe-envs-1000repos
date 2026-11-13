# Issue

**Title:** Update CI/CD for Python 3.7, 3.10, 3.13, 3.14 and fix compatibility issues

## Description

## Summary

Updates the GitHub CI/CD pipeline to test against Python 3.7, 3.10, 3.13, and 3.14, and fixes Python 3.13/3.14 compatibility issues in the codebase.

## Changes

### CI/CD Workflows
- **`.github/workflows/test.yaml`**: Updated test matrix from `[3.7, 3.8, 3.9, 3.10]` to `[3.7, 3.10, 3.13, 3.14]`. Updated `actions/checkout` to v4, added `actions/setup-python@v5`. Replaced deprecated `python setup.py sdist bdist_wheel` with `python -m build`.
- **`.github/workflows/deploy-pypi.yaml`**: Updated `actions/setup-python` from v1 to v5, bumped deploy Python from 3.7 to 3.10, replaced `python setup.py sdist bdist_wheel` with `python -m build`.

### Python 3.13/3.14 Compatibility Fixes
- **`agfusion/cli.py`**: Replaced 3 occurrences of deprecated `logger.warn()` with `logger.warning()` (removed in Python 3.12+). Removed `future` package import (`from future.standard_library import install_aliases`) — this was a Python 2/3 compatibility layer that is unnecessary for Python 3.
- **`agfusion/parsers.py`**: Replaced 1 occurrence of deprecated `logger.warn()` with `logger.warning()`.

### Dependency & Build Config
- **`setup.py`**: Removed `future>=0.16.0` from `install_requires`.
- **`requirements.txt`**: Removed `future>=0.16.0`.
- **`pyproject.toml`**: Added PEP 517/518 `[build-system]` configuration. Updated black `target-version` to `['py37', 'py310', 'py311', 'py312', 'py313']`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bc113cc3773b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.