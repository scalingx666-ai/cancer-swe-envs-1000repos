# Issue

**Title:** Add AMRFinderPlus

## Description

Add AMRFinderPlus component programs. The main tool launches other tools like BLAST with exec(), so that one can't be compiled, but users can call those other tools themselves as needed.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `315ab0bbfd77`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.