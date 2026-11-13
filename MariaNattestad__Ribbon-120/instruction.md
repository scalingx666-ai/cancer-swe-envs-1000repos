# Issue

**Title:** Improve VCF parsing

## Description

Update VCF parsing to work with the DRAGEN VCF in the examples:
https://v2.genomeribbon.com/?session=example:giab_hg008_dragen#splitthreader

That means testing with this VCF: https://42basepairs.com/browse/s3/giab/data_somatic/HG008/Liss_lab/analysis/DRAGEN-v4.2.4_ILMN-WGS_20240312/standard/dragen_4.2.4_HG008-mosaic_tumor.sv.vcf.gz

This parses several major variant types with different signatures that I could find in that sample dataset.

It's difficult to fully cover all the same information that we used to get from previous SV call sets. Specifically, I didn't try to parse the number of split reads from the SR in the SAMPLE columns because there are both tumor and normal samples, so it gets a little complex and I don't know how consistent that will be for other VCFs.

Added tests that can be run through `npm run test`.
![Screenshot 2024-09-17 at 9 41 11 AM](https://github.com/user-attachments/assets/946bd873-f985-4897-962c-f88b7f5a0451)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `65b818b68909`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.