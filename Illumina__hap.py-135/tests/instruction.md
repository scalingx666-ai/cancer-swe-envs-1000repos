# Issue

**Title:** Fixing argument namespace issue introduced with hguturu:hg-fix-pre-convert-gvcf

## Description

Fixing issue with `args.convert_gvcf_truth` missing from namespace in verion 0.3.13, described in 

To fix the issue I added `--convert-gvcf-truth` and `--convert-gvcf-query` arguments  to `hap.py`.
Potential issue with hap.py having both `--convert-to-vcf` and `--convert-gvcf-[truth|query]`. 
Added conditional statement and defining new variables `convert_gvcf_truth` and `convert_gvcf_query` so that the gvcf to vcf conversion is performed if either `convert_gvcf_to_vcf` or `convert_gvcf_[truth|query]` flags are used.

Please merge this pull request, or another fix, and release a new version for

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `214ec68253d2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.