# Issue

**Title:** Speed up sequence comparisons and targeted VCF scans

## Description

Two changes:

- Use the best edit distance so far to limit repeated sequence alignments.
- Start streaming near the first BED region instead of reading from the beginning of the chromosome.

On HG002 callsets, bench and collapse were about 11% faster. A 1 Mb chr1 target in a whole-genome VCF went from 6.67 to 0.93 seconds. Result files match . Tested with 5.5.1, pylint 10/10.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fa97db45fd8a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.