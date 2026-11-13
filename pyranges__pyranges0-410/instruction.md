# Issue

**Title:** Make doctest table formatting independent of terminal width

## Description

Running `pytest --doctest-modules pyranges` in a narrow or headless environment can hide table columns and fail doctests, even though the values are unchanged. GitHub CI masked this because the formatter forces a 250-column width whenever `GITHUB_ACTIONS` is set.

Set `COLUMNS=250` in an autouse fixture restricted to doctest items. Ordinary tests and normal library display keep their existing settings. Run CI doctests with `GITHUB_ACTIONS` unset and an initial 80-column width so the GitHub-only workaround can no longer hide this regression.

Validation:
- Reproduced the reported `GenomicFeaturesMethods.tss` failure at `COLUMNS=80` with `GITHUB_ACTIONS` unset.
- After the fix, all 87 doctests and 40 unit tests pass under those conditions on both pandas 2.3.3 and 3.0.6.
- Confirmed that `COLUMNS=250 pytest --doctest-modules pyranges` is a working workaround for the existing 0.1.6 source (87 passed).
- Black, isort and `git diff --check` pass for the change.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2ee368b38649`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.