# Issue

**Title:** Skip/ignore NA values at SNV/CNV logic checks

## Description

- small changes in `cnvsToStories()` and `extractClonalities()` in order to force superFreq to finish when NA values exist
- @ChristofferFlensburg mentioned he would like to add warning message when this happens
- references discussion in #53

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f313fddf2c67`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.