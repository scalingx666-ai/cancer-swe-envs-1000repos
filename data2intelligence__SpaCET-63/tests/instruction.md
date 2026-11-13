# Issue

**Title:** Add SpaCET.deconvolution.bulk.matched.scRNAseq for unmatched bulk RNA-seq

## Description

## Summary

Adds a single-call entry point for deconvolving bulk RNA-seq cohorts (e.g. TCGA) against a scRNAseq atlas, restoring a bulk pipeline using the algorithmically-correct path:

- **`SpaCET.deconvolution.bulk.matched.scRNAseq()`** — wraps the bulk count matrix into a minimal SpaCET object (placeholder coordinates, `platform = "Bulk"`) and dispatches to `SpaCET.deconvolution.matched.scRNAseq` with `sc_includeMalignant = TRUE`.

## Why this design

A bulk function existed in earlier work (commits prior to `6a46eb8`) but was removed because it inherited the malignant-first CNA cascade from `SpaCET.deconvolution`. The cascade is appropriate for spot-scale (1–100 cells per spot) but not for bulk samples that aggregate over millions of cells.

This new function intentionally exposes only the matched-scRNAseq joint hierarchical NNLS path:

- No malignant-first CNA cascade
- No within-cohort purity rescaling
- Malignant cells deconvolved jointly with non-malignant types when present in the reference

The "matched" in the function name refers to the **algorithm** (joint NNLS against a scRNAseq reference) rather than to patient identity. The reference does not need to come from the same individuals as the bulk samples — what matters is that it covers all relevant cell types at sufficient resolution. This makes it the right entry point for unmatched-bulk applications such as TCGA + an external scRNAseq atlas.

## What's in the PR

- `R/extensions.R` — new function `SpaCET.deconvolution.bulk.matched.scRNAseq` (135 lines incl. roxygen)
- `NAMESPACE` — export entry
- `man/SpaCET.deconvolution.bulk.matched.scRNAseq.Rd` — generated man page

No changes to the spatial pipeline. No new dependencies.

## Validation

This was validated against the matched Python implementation in [psychemistz/spatial-gpu](https://github.com/psychemistz/spatial-gpu) on the Wu et al. 2021 BRCA atlas, with subject-level train/test splits (see `docs/run_full_tutorial_t8_real_brca.py` and the rendered benchmark at https://psychemistz.github.io/spatial-gpu/bulk_benchmark.html).

## Test plan
- [ ] `R CMD check` passes locally
- [ ] Run on small example: deconvolve a 200-sample synthetic bulk against a 1000-cell scRNAseq reference, verify proportions sum to ~1 per sample and rough recovery of ground truth
- [ ] Verify backwards compatibility: existing `SpaCET.deconvolution.matched.scRNAseq` calls behave identically

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e8aee9069ebd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.