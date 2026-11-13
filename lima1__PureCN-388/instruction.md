# Issue

**Title:** If log ratios are provided, subset also the normals if available

## Description

Otherwise the filtering only on tumor samples may cause a misalignment the moment they're compared with the (unfiltered) normals.

Tested locally, the error is no longer present.

.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dfaa2319a3c2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.