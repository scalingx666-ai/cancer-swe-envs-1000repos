# Issue

**Title:** 1.6 Bugfix for BAM supplemented indexing

## Description

Fixes a minor bug introduced by moving of BAM modules from BioAlignments to XAM, where whippet-index.jl now needs to specifically load XAM.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b2523199707e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.