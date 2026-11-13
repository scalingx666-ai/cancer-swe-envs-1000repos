# Issue

**Title:** Unify the CLI subcommands

## Description

Makes the subcommands consistent and removes repeated code. The text output and the Python functions don't change.

- **Same `--json` output for all the subcommands**: `ok`, `errors` and `warnings`, plus the command's own data (e.g. `workflows`, `models`, `config`). `validate-config` gets `--json` too.

I'll open a PR in BiaPy-doc with the updated documentation.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6eeaf2c22e7e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.