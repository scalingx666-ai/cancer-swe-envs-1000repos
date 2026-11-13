# Issue

**Title:** Fix v1.5.0 review findings

## Description

## Summary
- Fix v1.5.0 review findings: COSMIC catalogue validation fixes, dashboard upload/process-identity/shutdown hardening, and CLI custom-text parsing fixes.
- Accept R row-name matrix exports whose header omits the mutation-context column, inferred only when the data proves the one-field shift; a genuinely wrong first column is still rejected.
- Canonicalize the legacy ID89 `Del(C):R(6,9)` repeat-interval label to the reference `Del(C):R(6,)`.
- Omit, with a visible dashboard warning (surfaced via `/api/matrix` and the UI), ID476 signature columns R-padded with `NA` for an unresolved (83-of-476) or entirely missing context, instead of zero-filling values that were never measured at that resolution; any other `NA` pattern is rejected as a corrupted matrix.

See `CHANGELOG.md` under `[Unreleased]` for the full itemized list.

## Test plan
- [x] `python3 -m pytest -q` -- 320 passed, 2 skipped
- [x] `ruff check` on changed modules -- clean
- [x] `python3 -m build --wheel` -- builds successfully
- [x] Verified against the real Liu et al. type89/type476 signature matrices (read-only, not committed): ID89 loads 89 labels/45 usable columns with 0 warnings; ID476 loads 476 labels/34 usable columns with the two expected omission warnings; `render_sample` succeeds for a representative signature from each.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `44e1914beea3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.