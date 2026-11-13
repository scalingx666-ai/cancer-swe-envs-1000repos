# Issue

**Title:** Update conversion documentation

## Description

Based on [a recent topic in the poppr forum](https://groups.google.com/d/msg/poppr/2L97Uko-FK8/YgOFAbucAgAJ), it has come to my attention that there is no documentation of  why `return.alleles = TRUE` is needed, so I have added it here and I will add it to the next poppr release.

I have also added the conditional in the examples to check if adegenet is loaded since you have it in Suggests, but not Imports.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0532d573673c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.