# Issue

**Title:** Allow paths/filenames with spaces when calling samtools

## Description

In createTHetAExomeInput.py, quote the filename arguments inside each call to os.system to prevent the shell from parsing the space-containing argument as multiple tokens (i.e. garbage).

Alternative solutions not attempted here:
1. use subprocess & avoid using the shell altogether; or
2. use pysam & avoid creating the pileup files on disk.

Also fixed a typo.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c88ed88fbdd6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.