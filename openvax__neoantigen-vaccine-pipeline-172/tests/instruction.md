# Issue

**Title:** Reenabling PDF outputs for OpenVax pipeline and a few other small fixes

## Description

- Fixing how Strelka2 is called, and removing unused old Strelka config file
- Using conda forge in the Docker container instead of miniconda for licensing reasons
- Fixing the example input config to use mhcflurry rather than the now unsupported netmhcpan-iedb MHC predictor
- Note that the PDF support here is a bit convoluted - a later version of Vaxrank does this more cleanly, and once we're ready to upgrade Vaxrank substantially, we can simplify some of this PDF logic here

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ee71eecbd9f0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.