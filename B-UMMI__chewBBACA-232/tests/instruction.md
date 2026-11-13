# Issue

**Title:** Prep external schema v351 bug

## Description

Fix the following bugs introduced in v3.5.1:

- Fixed issue in the PrepExternalSchema module related to the addition of loci prefixes to sequence headers when the original schema did not use prefixes (e.g., schemas from [cgMLST.org](https://www.cgmlst.org/ncs)).
- Fixed issue in the PrepExternalSchema module related to saving some alleles to the final FASTA files in the incorrect orientation.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `10b072bc949c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.