# Issue

**Title:** changed pre.py params to work with single gvcf

## Description

pre.py was crashing since it was expecting two args `convert_gvcf_truth` and `convert_gvcf_query` but referencing `convert_gvcf` since running pre.py directly only has one input. Updated the code and the documentation to use a single arg `convert_gvcf_to_vcf`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9d128a99e85b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.