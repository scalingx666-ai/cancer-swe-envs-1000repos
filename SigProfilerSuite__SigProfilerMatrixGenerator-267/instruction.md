# Issue

**Title:** Install the Workbench with uv, and prepare the 1.6.0 changelog

## Description

## Summary

Two commits: the Workbench's launcher installs with uv, and the changelog is prepared for 1.6.0.

### Installing with uv

The Workbench's launcher now installs its dependencies with [uv](https://docs.astral.sh/uv/) instead of pip, as the SigProfilerExtractor Workbench does. This commit was pushed to `feature/web-dashboard` just as #266 was merged, so it missed that merge.

- The launcher uses the `uv` on PATH; otherwise it adds uv to the Workbench's own environment with pip. It then installs with `uv pip install --python <environment's python> -e <repository>`.
- If uv cannot be added or cannot install, the launcher says so and falls back to pip, as before.
- `SPMG_WEB_INSTALLER=pip` always uses pip, for networks that only allow pip's configured package mirror.
- The fingerprint check is unchanged: nothing is installed when the packaging files have not changed.

Only `SigProfilerMatrixGenerator/web/launcher.py` changes in the package. Matrix generation is untouched.

## Timing

macOS, Python 3.13, no uv on PATH (so the uv numbers include adding uv), the launcher's own install command on throwaway environments:

| Install | pip | uv |
|---|---|---|
| First install, empty download caches | 47 s | 41 s |
| Reinstall, caches filled | 27 s | 4 s |

SigProfilerMatrixGenerator's dependencies are smaller than SigProfilerExtractor's (no PyTorch), so the first install gains less than there; reinstalls, for example after updating the repository, gain the most. The environment installed with uv imports SigProfilerMatrixGenerator from the repository (editable) and records its fingerprint.

## Docs

The Workbench guide describes the installer, the pip override, and uv's download cache in "What gets installed, and where" (not removed by the uninstaller; `uv cache clean` empties it). The README mentions uv in the start-up steps.

## Testing

| Suite | Result |
|---|---|
| `tests/web/test_launcher.py`: 7 new tests (uv on PATH, uv added, fallback when uv cannot be added or cannot install, `SPMG_WEB_INSTALLER=pip`, no fingerprint after a failed install, no install when the fingerprint matches) | 24 passed |
| `tests/web` + `tests/controllers` with Playwright and Chromium | 254 passed |
| Full suite (shared environment, browser tests skip) | 1,562 passed, 10 skipped |
| `mkdocs build --strict` | clean |

The new tests record the install commands instead of running them. The launcher jobs in `web-dashboard-launchers.yml` (macOS, Windows) exercise the real first install and the second launch that installs nothing.

## Changelog for 1.6.0

`CHANGELOG.md` gains a **1.6.0** section: the Workbench (#266), its uninstallers, the `web` entry points and the `web-tests` extra, and installing with uv.

The changes that sat under Unreleased had in fact shipped in earlier releases: the changelog was not split at release time after 1.3.6. They are now sorted into the releases that shipped them, using the changelog as it stood at each tag:

| Section | Entries | How it was decided |
|---|---|---|
| 1.4.0 (2026-10-02) | 32 | under Unreleased at the `v1.4.0` tag |
| 1.5.0 (2026-11-06) | 16 | added between `v1.4.0` and `v1.5.0` (no earlier entry was edited) |
| 1.5.1 (2026-11-10) | 1, new | the only change since 1.5.0, the MAF insertion anchor fix (#264), which was not recorded |

Every earlier entry is kept word for word.

## Release after merging

Tag `v1.6.0` on master with the "Create version tag" workflow, which publishes to TestPyPI; publishing a GitHub Release for the tag then publishes to PyPI, after approval of the `pypi` environment.

Note: PyPI's latest is still **1.4.0**. The v1.5.0 PyPI publish (release workflow run 42334068078) has been waiting for approval of the `pypi` environment since 2026-11-07, and 1.5.1 has a tag but no GitHub Release.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `73f9e8375dcd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.