# Issue

**Title:** fix: read RNA-seq annotation from FTP mirror

## Description

NCBI blocks the shared RNA-seq gene annotation download (`/geo/download/?...&file=<Species>.<build>.annot.tsv.gz`, with no `acc=`) behind a Google reCAPTCHA page, whatever the user agent. #230 made that failure clear; this PR fixes it.

- `readRNAQuantAnnotation()` reads the copy at `ftp.ncbi.nlm.nih.gov/geo/rnaseq_counts/annot/<file>` when one exists (human only today). Otherwise it falls back to the web URL and #230's `geoquery_ncbi_challenge` error.
- Version bumped to 2.81.35, with NEWS.

Verified: `getRNASeqData("GSE145842")` returns 39376 x 23, and `test_rnaseq_helpers.R` and the live `test_geo_rnaseq.R` pass.

Known limit: mouse (`Mouse.GRCm39.annot.tsv.gz`) is not on the FTP mirror, so mouse series still get the clear error.

. Partially addresses #230 (human only; mouse remains blocked).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3840ff4e4efc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.