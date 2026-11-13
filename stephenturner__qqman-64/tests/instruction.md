# Issue

**Title:** make annotatePval and annotateTop work with logp=FALSE

## Description

Hello Stephen,
Here is a pull request where I changed the code of the `manhattan` function (and its doc) so that, when `logp=FALSE`, SNPs can be annotated if their value from the `P` column is above the threshold given by `annotatePval`, and not below.
I think it can be merged as such and the version incremented to 0.1.7.
Best,
Tim

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3cdfa9a6a786`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.