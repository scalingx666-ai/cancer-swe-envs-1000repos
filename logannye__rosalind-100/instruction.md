# Issue

**Title:** Fix RC contract discovery for analyzer value enums

## Description

The RC contract snapshot currently refuses the maintained CLI inventory because `analyze <KIND>` uses a positional value enum rather than Clap subcommands. Discover its supported kinds from the actual help output, expanding only the `analyze` parent so repeated leaf help cannot recurse.

Include argument and option possible values in canonical CLI fingerprints, while continuing to ignore descriptive wording and wrapping. The release policy inventory and publication gates remain intact.

Validation: all 33 xtask tests pass, including a fake CLI regression for exact analyzer discovery and wrapped enum-fingerprint changes; xtask clippy with warnings denied and whitespace checks pass.

Actual candidate validation: `contract snapshot` succeeds at `5c4b027dee116d8d4b3ebfb14fff2731f4e09681` with 52 components, including all four analyzer kinds. `rc plan --version 0.5.0 --number 1` passes the contract snapshot and remains blocked only because this PR commit is not yet reachable from `origin/main`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7d58d42ff5a0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.