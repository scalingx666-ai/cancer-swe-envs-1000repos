# Issue

**Title:** fixing BND conversion

## Description

I think the 5to5 and 3to3 breakpoint conversions may have been a bit off in their notation.

Here, I've tried to fix this. I've altered the 5to5 and 3to3 to resemble what is shown in section 5.4 of https://samtools.github.io/hts-specs/VCFv4.5.pdf

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `48c475d86e32`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.