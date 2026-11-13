# Issue

**Title:** Add region_match to pairtools_select

## Description

Addresses #277 
Allows to filter pairs by coordinates, e.g. 
`pairtools select 'region_match(chrom1, pos1, "chr1", 100, 500) and region_match(chrom2, pos2, "chr1", 100, 500)'`

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7e69d6cfdb72`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.