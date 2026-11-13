# Issue

**Title:** v1.3

## Description

Version 1.3_r1 supports both python3 and python2. This release also corrects a bug in the visualization of amplicon copy numbers for genome segments < 50kbp and includes small improvements to seed filtering and merging of nearby segments. Complete changelog available [here](https://docs.google.com/document/d/1tGwKcHgaU36OzMZ02S5ky5JR-67WvRtXI3-Hv0FYkm4/edit?usp=sharing).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `446950f0cdf3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.