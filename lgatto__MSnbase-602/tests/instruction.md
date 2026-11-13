# Issue

**Title:** fix: disable nested parallel processing for chromatograms

## Description

This fix addresses a comment in issue


`chromatogram()` is extracting chromatograms in parallel for each sample/file. The internal function uses `spectra()` to load the data in each parallel process. The default value for `BPPARAM` of `spectra()` is however `BPPARAM = bpparam()`, thus, an eventual nested (and unnecessary) parallel processing setup is created. This PR forces the internal `spectra()` call to disable parallel processing.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6284cc657038`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.