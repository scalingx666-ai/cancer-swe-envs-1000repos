# Issue

**Title:** [RELEASE_3_23] fix: read RNA-seq annotation from FTP mirror

## Description

Backport of #236 to RELEASE_3_23, bumping the version to 2.80.1 so the fix propagates to Bioconductor release.

This is the same change as #236, except it calls `httr2::request()` directly because release has no `.geo_request()` helper. The regression test is in a new `test_rnaseq_annotation.R` because release has no `test_rnaseq_helpers.R`.

Verified on this branch: `getRNASeqData("GSE145842")` returns 39376 x 23, and the new test plus the live `test_geo_rnaseq.R` pass.

 on release.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8b846af9fe72`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.