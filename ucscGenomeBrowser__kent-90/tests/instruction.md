# Issue

**Title:** added a -namePrefix option to faToTwoBit which will prefix the sequence names with the argument string in the resulting 2bit file

## Description

added a -namePrefix option to faToTwoBit which will prefix the sequence names with the argument string in the resulting 2bit file
for instance:
    faToTwoBit -namePrefix=hg38. <(gzip -cdfq hg38.analysisSet.fa.gz) hg38.2bit
    the hg38.2bit file will have sequence names like "hg38.chr1" instead of just "chr1".
    
the sequence file above is located here: https://hgdownload.soe.ucsc.edu/goldenPath/hg38/bigZips/analysisSet/hg38.analysisSet.fa.gz

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ce8f3ea0b9a9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.