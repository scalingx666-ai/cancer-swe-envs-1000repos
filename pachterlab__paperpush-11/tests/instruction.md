# Issue

**Title:** Replace portal-drift tests with a scheduled full submit walkthrough

## Description

## Why

The portal-drift tests checked only the login page and the first form page of a portal, and only bioRxiv and Bioinformatics had specs. Bioinformatics had no committed baseline and is usually blocked by Cloudflare, so in practice they watched one page of one portal. A change on any later page went unnoticed. The full walkthrough already covers every page of every venue with a runner, so the scheduled check should run that instead.

## What changed

**Removed**
- `tests/test_portal_drift.py`, `tests/drift.py`, `tests/portal_snapshots/`
- the `--update-snapshots` option and `update_snapshots` fixture in `tests/conftest.py`
- `capture_failure` in `paperpush/venues/common.py` (only the drift tests used it)
- the drift step in the `paperpush-add-venue` skill (both copies) and the snapshot docs in `DEVELOPMENT.md`

**Added**
- `scripts/check_submit_walkthrough.py` runs `tests/test_submit.py::test_submit_walkthrough` without `-s`, so venues run back to back. It writes `.submit_walkthrough/report.md` and `report.json`, and opens an issue labelled `submit-walkthrough` for venues that failed all three attempts, or comments on the one already open. It never closes issues. A run longer than 4 hours is interrupted, and the venues it finished are still reported. `--dry-run`, `--venue`, `--headless` and `--junit` are supported.
- `scripts/scheduled_submit_walkthrough.sh` is the scheduled entry point. It runs against a detached `origin/main` worktree, with headed browsers on macOS and `xvfb-run` on Linux, and works on both (it uses an mkdir lock where `flock` is missing).
- `tests/test_check_submit_walkthrough.py`: 7 offline tests (junit parsing, report, issue open/comment logic, pytest invocation).
- A "Scheduled submit walkthrough" section in `DEVELOPMENT.md`.

Each scheduled run leaves an unsent draft on every portal, and an expired login shows up as a failure.

## Testing

- Offline suite: 2601 passed, 60 skipped
- `gen_readme_venues`, `gen_venues_schema`, `gen_schema_docs`, `gen_subfile_templates`, `sync_agent_docs` `--check` all pass
- The walkthrough collects all 26 cases from a fresh `origin/main` checkout. The scheduled run itself was not run end to end (it would leave drafts on every portal).

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ed0f4cf9efea`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.