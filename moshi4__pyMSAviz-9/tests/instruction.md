# Issue

**Title:** Bump to v0.4.1

## Description

# Change Log

### Improvement

- Added `--label_type` option to CLI
- Fixed `mv.savefig()` to suppress memory leak during multiple plots
- Changed linter `flake8` to `ruff`
- Changed `set_layout_engine()` to `tight_layout()` for matplotlib backward compatibility (#7)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `546869c4fe01`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.