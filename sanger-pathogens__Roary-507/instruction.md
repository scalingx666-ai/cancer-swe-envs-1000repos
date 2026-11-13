# Issue

**Title:** fixed error by old pandas version

## Description

newer pandas version use `.loc` rather than `.ix`
see: https://pandas.pydata.org/pandas-docs/version/0.23.4/generated/pandas.DataFrame.ix.html fore more info.

same goes for matplotlib from `axisbg` to `facecolor`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `adaef937daac`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.