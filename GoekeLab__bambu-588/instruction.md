# Issue

**Title:** Fix bambu requiring internet access when given a local FASTA genome path

## Description

## Summary
- : `bambu()` failed on offline machines (e.g. an offline HPC cluster, or a self-contained biocontainers image with no internet egress — see ) even when given a plain local FASTA file path for `genome`.
- Root cause: `checkInputSequence()` in `R/bambu_utilityFunctions.R` unconditionally called `BSgenome::available.genomes()` for any character `genome` argument, before ever checking whether the string was simply a local file path. That call reaches out to Bioconductor's package repository over the network, so it threw a raw Bioconductor/BiocManager error instead of just reading the FASTA.
- Fix: only attempt the `BSgenome::available.genomes()` / `getBSgenome()` lookup when the string is **not** an existing local file, and wrap that lookup in `tryCatch` so a blocked/failed network call falls through to the existing FASTA-read path (and its existing clear error message) instead of crashing.

## Test plan
- [x] `devtools::load_all()` + traced `BSgenome::available.genomes()` to confirm it is no longer called when `checkInputSequence()` is given the package's local test FASTA (`inst/extdata/Homo_sapiens.GRCh38.dna_sm.primary_assembly_chr9_1_1000000.fa`)
- [x] Confirmed a nonexistent path still produces the original `"Input genome file not readable."` error
- [x] `testthat::test_file()` passing locally for `test_bambu_arguments.R`, `test_scoreRC.R`, `test_isore.R` (all exercise `checkInputSequence()`/`bambu()` with a local FASTA path)
- [x] `test_setNDR.R` fails identically before and after this change (missing fixture path in this environment) — confirmed unrelated to this fix

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a445dcfb60b6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.