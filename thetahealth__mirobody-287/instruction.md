# Issue

**Title:** github: add a general bug report form and fix setup instructions

## Description

## Summary

Add a general **“Something does not work”** issue form for startup failures, broken pages and incorrect answers. These problems previously had only a blank issue, so reports often needed another round trip to obtain basic reproduction details.

The form requires the version, deployment method, model selection, reproduction steps and expected/actual behavior. It also offers optional host, `mirobody doctor` and log fields, with a required confirmation that no health data, keys or tokens were pasted. It points reporters toward synthetic demo files and accepts Chinese responses.

The existing wrong-term and upload-with-no-indicators forms keep their narrower roles.

## Corrections to existing forms

- Replace the unsupported `mirobody --version` command with the Python package/vocabulary versions or the running app's `server_version` at `/mirobody.json`.
- Use `docker compose up -d` after editing `.env`; `restart` retains the old container environment.
- Record the form and command changes under CHANGELOG Unreleased.

No Python or runtime behavior changes.

## Validation

- All four files in `.github/ISSUE_TEMPLATE/` parse as YAML. Form types, unique IDs, string options and required fields match GitHub's issue-form schema.
- The `bug` label exists, Discussions is enabled, and the documented Docker services and server-version endpoint exist.
- Executed the Python version command and checked doctor formatting with synthetic configuration: key names/status and model names are shown, not credential values.
- All Git-tracked Python tests: **1500 passed, 169 skipped, 12 xfailed**.
- Ruff, compileall and bare library imports passed; `lint-imports`: **6 kept, 0 broken**.

A plain `pytest -q` in the long-lived local checkout also discovers outdated, gitignored maintainer tests and stops with 23 collection errors from removed APIs/dependencies. The runtime source and test configuration are identical to `main`; the tracked suite above passes. These unrelated local tests were left unchanged.

The chooser's actual rendering can only be checked after the form reaches the default branch. Existing `resolver` and `extraction` labels referenced by the older forms are absent; this PR does not change those repository labels.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8087fddcbcbb`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.