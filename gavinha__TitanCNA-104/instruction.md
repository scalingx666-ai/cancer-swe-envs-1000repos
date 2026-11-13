# Issue

**Title:** Add purity/ploidy in plot title and plotCorrectedCN option

## Description

Adds a new --plotCorrectedCN CLI option (default TRUE) to control whether CN plots use corrected copy number, passed through to plotCNlogRByChr(). Also updates the combined genome-wide plot title to include purity and ploidy values.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b26d9f8aa84e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.