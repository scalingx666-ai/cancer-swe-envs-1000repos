# Issue

**Title:** Update Ensembl SO mappings, report VCF ref and alt alleles, and fix Perl deprecation

## Description

Hello! This PR brings `vcf2maf` up to speed with modern Ensembl Sequence Ontology (SO) terms, reports original VCF reference and alt alleles, and fixes a deprecation issue that breaks the script on newer Perl versions.

### Key Changes

* **Ensembl SO Term Updates:** Added missing terms (e.g., `splice_donor_region_variant`, `start_retained_variant`) and updated severity priorities to match Ensembl's current HIGH/MODERATE/LOW/MODIFIER impact hierarchy.
* **MAF Classification Fixes:** Updated regexes in `GetVariantClassification` so new splice variant correctly maps to `Splice_Region` and `start_retained_variant` maps to `Silent`.
* **Original VCF Allele Reporting:** Added `vcf_ref` and `vcf_alt` columns to the output MAF. *(Note: This was from a previous commit on my fork that I am including in this upstream PR).* This is highly helpful for connecting back to records in the VCF.
* **Perl 5.38+ Compatibility:** Replaced the deprecated smartmatch operator with a standard `grep` equivalent when deduplicating `@ann_cols`.

Tested locally against v115 VEP VCF output. Let me know if you need any adjustments to get this merged!

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ed0e3169349c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.