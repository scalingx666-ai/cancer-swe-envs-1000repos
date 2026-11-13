# Issue

**Title:** fall back to rsIDs carried in the VCF ID column so dbSNP_RS is still populated

## Description

If VEP couldn't find this variant in dbSNP/COSMIC/etc., or VEP did not run we'll say it's "novel"
however, it ignores the ID column in VCF which is expected to hold this information by the VCF standard.

In this PR vcf2maf will fall back to rsIDs carried in the VCF ID column so dbSNP_RS is still populated if VEP did not find the ID

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `589406f3a704`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.