# Issue

**Title:** Remove OSI Approved BSD License classifier

## Description

Removed OSI Approved BSD License classifier from project metadata.

Gentoo Linux QA complains and you already have the license in pyproject.toml license field.

```
 * QA Notice: setuptools warnings detected:
 * 
 * 	License classifiers are deprecated.
 * 	`project.license` as a TOML table is deprecated

```

EDIT: Apparently Github editor also removed trailing file newline...

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f6438ec185f5`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.