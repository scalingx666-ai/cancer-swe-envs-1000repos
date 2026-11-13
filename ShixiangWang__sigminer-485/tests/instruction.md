# Issue

**Title:** feat(p3): clean-room likelihood/lrt refit decision layers for sig_fit + bootstrap route (parity plan P3)

## Description

# P3 — clean-room refit methods for `sig_fit`: `method = "likelihood"` / `"lrt"` + parallel bootstrap route

Implements parity-plan row P3 (`docs/research/09-sigminer-v3-parity-plan.md:73`, msuiter checkout): MuSiCal-branch likelihood refit/selection and PASA/mSigAct-branch likelihood-ratio-test refit decisions as **opt-in** `sig_fit(method=)` extensions, plus the `sig_fit_bootstrap*` `method` pass-through (parallel batch route intact). Three commits off `master@37fc92a8` (post #484), 14 files, **+1241/−11**.

## Primary-source gate (ran BEFORE any implementation code)

Full record with verbatim quotations: lane log `00-primary-source-gate.md` (written pre-RED).

- `method = "likelihood"` ← **MuSiCal**: Jin, Gulhan, Geiger, Ben-Isvy, Geng, Ljungström et al., *Nature Genetics* 2024, DOI `10.1038/s41588-024-01659-0` — nested-model likelihood comparisons, bidirectional stepwise (backward drop iff removal cost < keep-line; forward re-admit iff gain ≥ add-line).
- `method = "lrt"` ← **PASA**: Jiang, Wu, Rozen, *Briefings in Bioinformatics* 2024, DOI `10.1093/bib/bbaf042` — λ = 2ΔlogL on χ² with df = signature-count difference ("the paper's own rule"), presence test, stop-LRT, minimality.
- Controller independently re-fetched both DOIs against the OpenAlex authoritative record (title/venue/authors/year match the gate record verbatim).

Clean-room law honored: semantics were taken from the papers' documented mathematics only; no code was copied from either tool's implementation. Where the papers under-specify a constant (defaults `ll_add = ll_keep = 8.0`, `alpha = 0.01`, the empty-set reference, the round guard), the code and Rd say so explicitly ("lane-calibrated", "not a paper element") — no invented semantics dressed as citations.

## What the decision layers do (`R/sig_fit_refit.R`, +350)

| Surface | Semantics | Pinned by |
|---|---|---|
| `method="likelihood"` | MuSiCal-style bidirectional stepwise over the candidate roster on the multinomial log-likelihood; numeric exposures still via the certified QP simplex (`decompose_QP` contract preserved) | `test-sig-fit-refit-likelihood.R` (defaults; `ll_add=1e9,ll_keep=-1` ≡ legacy; `ll_keep=1e9` re-admits) |
| `method="lrt"` | PASA-style: presence test (df=1), stop-LRT vs full set, minimality (every member removal `p < alpha`); first qualifying minimal set wins; exposures via the same QP refit | `test-sig-fit-refit-lrt.R` (α=0 clears board; α=1 ≡ legacy QP) |
| `sig_fit_bootstrap` / `_batch` | `method=` pass-through so bootstrap nulls follow the chosen decision layer; batch keeps `furrr_options(seed = TRUE)` worker reproducibility (`sig_fit_bootstrap_batch.R:166`); cross-arm **bit-identity is explicitly not the contract** — structural/significance/statistical agreement is (documented at `R/sig_fit_bootstrap_batch.R:166`) | `test-sig-fit-refit-bootstrap-par.R` (56 expectations) |

Preservation law held byte-for-byte: `method` default (`"QP"`) and every legacy string resolve and behave exactly as before; the two new arms are opt-in; `match.arg` house idiom, refusal text names all valid choices; `auto_reduce = TRUE` refusals ride the house `send_stop`/cli channel.

## Null calibration + flat-signature non-regression (MEASURED, a-priori ceilings)

198-cell M3b-protocol-shape fixtures (seeds `31337/71113/71114`; ceilings declared in the test source **before** measurement):

- **Null false-positive**: both methods, all six signatures `0.000`, any-decl `0.000` — inside the declared 0.10/0.20/0.30 ceilings.
- **Recall**: two-spike `1.000` (floor 0.90), single-spike `1.000` (floor 0.95) for both methods.
- **Flat-signature cells** (the documented SBS5/40 underestimation failure mode, cf. msuiter `docs/research/00-executive-summary.md:30`): legacy capture `0.9942`; `lrt` `1.0000`; `likelihood` `0.8750` — inside the a-priori 15-point band (`≥ 0.9942 − 0.15`) and above the 0.70 absolute floor; decoy capture `0.0000` (≤ 0.10 ceiling). No flat-cell regression vs the legacy route under the pre-registered law.
- Every numeric is hand-built (D3): a synthetic 30×6 roster (spike/flat/tilt/decoy), house simulator catalogs; **zero COSMIC-derived values** (the only "COSMIC" string in the added lines is the negative attestation comment).

## Battery (controller-replicated on detached replicas, identical ambient)

| arm | files | nb | failed | skipped | error | warning | passed |
|---|---|---|---|---|---|---|---|
| BASE `37fc92a8` | 60 | 805 | 0 | 6 | 1 | 211 | 588 |
| HEAD `d1fbb99b` | 65 | 971 | 0 | 6 | 1 | 211 | 754 |

Per-file diff: the symmetric difference is **exactly** the five new test files (166 expectations, all green); all 60 common rows are identical on both sides. The `error=1` cell (`test-roxytest-testexamples-get_sv.R`) is byte-identical on BASE — pre-existing host artifact, not touched by this branch. The six skips are the pre-existing rust-backend (5) + sigprofiler-matrix (1), identical both sides. TDD history: RED witness `files=5 nb=8 failed=6 error=26` (methods rejected by the pre-engine `match.arg`), GREEN witness `files=5 nb=166 failed=0`.

## Governance

- `NAMESPACE` / `DESCRIPTION` / `_pkgdown.yml` deltas: **0** (no new exports — decision layers are internal; `method` extension rides documented topics).
- The three touched `man/` topics' `\\link` targets all resolve against the `man/` alias union (mechanical predicate green); Rd edits hand-surgical.
- Attribution trailers: 0. Added-line CJK scan: 0 hits on a decoded scanner whose positive controls (Han + kana) demonstrably fired. R-floor (≥ 3.5.0) census over added lines: 0 post-floor constructs, 0 native pipes.
- `NEWS.md` entry carries **zero speed claims** (P6 owns measured performance tables).
- Floor `R >= 3.5.0` respected on every added line.

## Test plan

- [x] New family: `test-sig-fit-refit-{likelihood,lrt,bootstrap-par,flatcells,nullcal}.R` (166 expectations) — green in this table.
- [x] Legacy full suite: 60 common files verbatim vs BASE.
- [ ] CI: five arms green at check-run level (to be attested on this head post-open).

Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `37fc92a87272`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.