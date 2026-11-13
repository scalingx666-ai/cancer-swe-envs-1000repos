# Issue

**Title:** Version4 cpp

## Description

* [ ] Flake8 passes (`flake8 . --exclude=.venv,.build,planemo_test_env,build --ignore=E501,F403,E402,F999,F405,E712`)
* [ ] Local tests pass (`py.test hicexplorer --doctest-modules`)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `88cc9f1e5edc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.