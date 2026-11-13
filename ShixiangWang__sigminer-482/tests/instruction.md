# Issue

**Title:** P1: rust NMF backend -- isolated-process bridge to the certified msuiter KL-MU kernel (parity plan P1)

## Description

## Summary

Adds `backend = "rust"` to the three public NMF entry points (`sig_extract()`, `sig_estimate()`, `bp_extract_signatures()`), routing computation through an **isolated-process bridge** to msuiter's certified pure-Rust KL-MU NMF kernel (`msuiter-kernel fit-kl`, protocol = 1).

. The original request pointed at the `omicverse/rust-NMF` crate; that route was **declined on licensing grounds** (GPL-2.0+ against this MIT package; the crate is also not published on crates.io). The ruling is recorded in WangLabCSU/msuiter `docs/research/09-sigminer-v3-parity-plan.md` §7: no external GPL kernel is linked — the in-house Apache-2.0 certified engine (KL-MU kernel, ‖ΔW‖F/‖W‖F ~ 1e-15 vs its reference) is the backend, and `rust-NMF` is kept as an independent yardstick for the P6 benchmark campaign only. The isolated-process boundary means no GPL code is ever loaded into the host process, but the package policy is stated as-is.

## Contract and boundary

- Kernel handshake: `--version` pinned to the frozen protocol=1 shape (`protocol = 1`, finite `kl_eps`); run aborts on shape drift.
- Single execution seam `.kernel_exec()` → `system2()` with character-vector argv (no shell); inputs staged as `%.17e` CSVs, outputs (`W/H/trace/meta.csv`) parsed fail-closed (dims, finiteness, non-negativity, meta cross-checks, trace continuity, `iterations == iters`).
- Kernel resolution: `option(sigminer.rust_kernel)` → `MSUITER_KERNEL_BIN` → PATH, via `file.exists` probes (no OS-identity string branching).
- Runtime gate on the **optional** `msuiter` package: `.require_msuiter()` (requireNamespace, reticulate idiom) hard-fails with the install route `pak::pkg_install("WangLabCSU/msuiter")`. msuiter is not on CRAN, so a Suggests entry would hard-fail this repo's lockfile-based CI setup (forensics recorded in the ruling comment).
- Seed law: every replicate carries an explicit `--seed`/`--replicate`; `init = "external"` refuses multi-run fits.
- `match.arg()` validates `backend` before the R fallback — a typo can never silently downgrade rust → R.

## Wiring

| file | change |
|---|---|
| `R/rust_backend.R` | **new**: internal bridge surface (~580 lines, zero new exports; NAMESPACE unchanged) |
| `R/sig_extract.R` | `backend` arg; rust branch gated to KL(brunet); pynmf-exclusivity guard; R path byte-identical |
| `R/sig_estimate.R` | `backend` arg; `use_random`/`save_plots` fail-closed under rust; survey payload built from kernel outputs (same slot names) |
| `R/best_practice.R` | `backend` arg; parallel `n_run` inside the existing future fan-out; explicit per-replicate seeds; cache keys salted per backend (`_RUST_K` vs `_NMF_K`) |
| DESCRIPTION | unchanged (see the CI lockfile ruling below — msuiter is documented, runtime-gated, not a Suggests entry) |
| `NEWS.md` | feature entry only — **no timing claims** (benchmark numbers are owned by the P6 evidence loop) |

## Tests (TDD: R-path goldens snapshotted before wiring; RED battery committed before the boundary)

`tests/testthat/test-rust-backend.R` — 33 units: 28 always-on (mock injection at the single seam: argv goldens, fail-closed matrix/meta/trace handling, tamper loops, backend validation incl. partial-match refusal, seed law, `init = "seeded"` zero-lock, `init = "nndsvd"` G2 regression, thread-count invariance workers 1/2, R-path preservation replay) + 5 live-kernel units gated on `MSUITER_TEST_KERNEL_BIN` (incl. bit-equivalence vs `NMF::nmf(brunet)` at ‖ΔW‖F/‖W‖F < 1e-10 under a `NMF >= 1.5` version gate, and output-shape equality vs the live R path).

Evidence (reviewer independently re-ran all of it):

- mock battery (no kernel): `33 units / 0 fail / 0 err / 5 skip / 190 pass`
- live battery vs pinned msuiter-trunk kernel: `33 / 0 / 0 / 1 skip / 217 pass` (the 1 skip is the NMF version gate; CRAN arms run it)
- full suite: `UNITS=109 FAILED=0 ERROR=1 SKIP=6 PASS=462` — the sole error is pre-existing and byte-identical at base `e5975f13` (`test-roxytest-testexamples-get_sv.R`, `expect_is()` deprecation under edition 3; CI does not install roxytest, where the file skips)

## Compliance

- **D3**: all fixtures synthetic (powers-of-two dims); no COSMIC numerics anywhere in the diff.
- **R floor**: no `%||%` in any new code (base-only from R 4.4.0 vs package floor 3.5.0) — repo-wide `-F` scan zero hits; helpers use floor-safe idioms.
- Zero new exports; MIT license untouched; roxygen documented, `.Rd` regenerated.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e5975f139e1f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.