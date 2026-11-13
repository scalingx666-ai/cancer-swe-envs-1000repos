# Issue

**Title:** chore: drop version from CITATION.cff and its update workflow

## Description

Stops the CITATION.cff bump PR that came after every release (#860, #864, #874).

- Remove `version` and `date-released` from `CITATION.cff`. Both are optional in CFF 1.2.0. GitHub's "Cite this repository" uses `preferred-citation`, the iMeta paper, so they were barely used.
- Delete `.github/workflows/update-citation-cff.yml`, which opened a PR on every `v*` tag to bump those two fields.

`cffconvert --validate`: valid under schema 1.2.0.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_019mN8ixeibi7qiB4PzhMo1Y

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `687c5d3e62f9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.