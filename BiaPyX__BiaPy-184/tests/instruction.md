# Issue

**Title:** Add schema_version and data to --json output, and CLI tests

## Description

- The `--json` output of the subcommands now has `schema_version` and puts each command's data in `data`. Text output and Python functions don't change.
- Adds `tests/test_cli.py`: tests of the seven subcommands (JSON, text and exit codes), with synthetic data, no GPU or internet.
- AGENTS.md: lists the subcommands and the new test.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9442f96545da`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.