# Issue

**Title:** feat(p2): bp-route K arbitration -- port of the certified msuiter ms_select_k survey (parity plan P2)

## Description

## What

Parity plan **P2** (umbrella msuiter#1; tracked by ): port of the certified msuiter `ms_select_k()` three-layer K arbitration into sigminer's best-practice route.

- **New export `bp_select_k(counts, k_grid = 2:5, ...)`** -- standalone raising surface: layer 1 SUITOR-style fold CV deviance argmin, layer 2 stability veto (`avg >= 0.8`, `min_cluster >= 0.2`, `sum >= 1.0`, verbatim from the reference), layer 3 diagnostic Wilcoxon. Evidence-table contract validated at the boundary.
- **Opt-in route hook**: `bp_extract_signatures(..., k_select = c("legacy", "arbitrate"))` -- trailing defaulted arg; `"legacy"` (default) keeps the extraction and its `suggested` ranking **byte-for-byte**; `"arbitrate"` annotates `k_evidence`, preserves the old suggestion under `suggested_legacy`, and reports the arbitrated rank with degrade semantics (annotation never errors the extraction; the standalone surface raises instead, mirroring the reference pipeline's raise-vs-degrade mode axis).
- **Reference implementation**: msuiter `R/kselect-select.R` @ `dad3044` (P1-landed trunk). Thresholds, fallback scan order (CV-error ascending, NA-last, rank tiebreak) and veto reason strings are verbatim ports, not reinterpretations.

## Parity evidence (all numbers from logged controller runs)

- **Bit-exact reference replay**: committed `msuiter_core_cases.rds` captures (S1..S7 hand-built evidence frames run through the msuiter reference core on the controller host) -- the ported core reproduces every verdict; fixtures are **msuiter-absent-safe** (plain data, `readRDS` only, zero reference-package presence at check time; regeneration is controller-side only -- CI lockfile law).
- **Seed law**: single root seed `20261015`; every NMF fit is pure in (data, k, seed) via the documented LCG-derived stream (same 16807 / 2^31-1 family as the reference, IEEE-exact intermediates); rerun byte-identity pinned.
- **D3**: every committed number is synthetic (Park-Miller LCG cells, pinned seeds); no COSMIC-derived numerics.

## Controller zero-regression attestation (own hands)

| suite | files | tests | failed | error | passed | warn | skip |
|---|---|---|---|---|---|---|---|
| base `1e174a04` | 57 | 679 | 0 | 1 (pre-existing roxytest `get_sv`) | 462 | 211 | 6 |
| head `c09cfff4` | 60 | 805 | 0 | 1 (same) | 588 | 211 | 6 |

Per-file table diff = **exactly the three lane files, added only** (core 32, pipeline 66, replay 28 -- sum 126 = head-base test delta). Targeted lane files re-run by controller: 126/0/0. Governance: NAMESPACE delta `+export(bp_select_k)` only; DESCRIPTION untouched (no Suggests entry -- lockfile law); zero attribution trailers; zero CJK; R 3.5.0 floor census on added lines clean (`setdiff` at one call site matches >= 5 pre-existing trunk call sites incl. the bp hot path -- trunk-wide floor hygiene is a separate follow-up, not introduced here).

TDD lineage: RED core (10 errors) -> GREEN core 32/32 -> reference captures -> RED pipeline (7 errors) -> engine 66/66 -> generator fix. Six commits, 14 files, +1420/-3.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1e174a044e1e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.