# Issue

**Title:** slimmer image from Dockerfile

## Description

Hi Brent, I updated your Dockerfile to produce a smaller image. Plus I upped the versions of several components: libdeflate, htslib & bcftools. Still testing the changes with somalier, but everything seems to build ok.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a2013db8b619`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.