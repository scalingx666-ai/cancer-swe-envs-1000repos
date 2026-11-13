# Issue

**Title:** Remove redundant `trigger_all` workflow

## Description

With all 4 batch workflows (`all_1.yml`–`all_4.yml`) in place and each supporting `workflow_dispatch`, the top-level `all.yml` wrapper that simply re-dispatched to all four is no longer needed.

## Changes

- **Deleted** `.github/workflows/all.yml` — the "Trigger All Workflows" aggregator workflow

<!-- START COPILOT CODING AGENT TIPS -->
---

🔒 GitHub Advanced Security automatically protects Copilot coding agent pull requests. You can protect all pull requests by enabling Advanced Security for your repositories. [Learn more about Advanced Security.](https://gh.io/cca-advanced-security)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `63147e17efb3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.