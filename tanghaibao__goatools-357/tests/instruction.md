# Issue

**Title:** Fix local Holm and Sidak adjusted p-values

## Description

Found while triaging #309. `holm` and `sidak` are in `find_enrichment`'s default `--method` list, and both resolve to the local implementations.

## Bugs
- **`holm` could report adjusted p-values that were too small.** It scaled the i-th smallest p-value by (n − i) but skipped Holm's step-down maximum, so a later p-value could end up below an earlier one. `[0.03, 0.04]` gave `[0.06, 0.04]` instead of `[0.06, 0.06]`, which makes terms look more significant than Holm allows. The existing test asserted the wrong value.
- **`sidak` reported scaled p-values, not Sidak-adjusted ones.** It multiplied by `α/(1−(1−α)^(1/n))`, which matches Sidak's decision only at exactly α. For example, p=0.2 with n=4 reported 0.785 instead of 0.590.

## Fix
- **Holm:** sort the p-values, scale by (n − i), and take the running maximum.
- **Sidak:** `1 − (1 − p)^n`.

Both now match `statsmodels.stats.multitest.multipletests`, including ties, p = 0, p = 1 and empty input. Bonferroni was already correct.

## Tests
- **`test_multiple_testing.py`:** fixes the expected Holm value and adds a statsmodels comparison for holm, sidak and bonferroni over random vectors with ties. Holm and Sidak fail on `main`.
- **CI subset:** 198 passed, 12 skipped.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01YaTHwoZmywheAEUdp4zJtb

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5d207c536b20`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.