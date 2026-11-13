# Issue

**Title:** Upgrade CircleCI config from version 2 to 2.1

## Description

## Summary

- Upgrade CircleCI config version from 2 (EOL) to 2.1
- Remove the now-unnecessary `version: 2` under `workflows`
- Update doc links from `/docs/2.0/` to `/docs/`

Config version 2 reached end of life on July 17, 2026:
https://discuss.circleci.com/t/breaking-changes-config-compilation-updates-july-17-2026/54719

## Test plan

- [ ] CircleCI pipeline runs successfully on this PR's branch

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01SjL1eZZB5o2D7URjVQAe2E

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `18763f8eee86`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.