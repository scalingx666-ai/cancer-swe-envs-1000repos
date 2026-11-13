# Issue

**Title:** Skipping NA in SNVs/CNVs in superFreq v1.4

## Description

New pull request after #54 needed to be reverted in order to incorporate @ChristofferFlensburg's new updates to be released in v1.4

- updates without this patch was tested on the same samples used when the original issue arose (#53) and failed
- updates with this patch was tested on the samples mentioned above and everything passed!

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9ba020ed1f5e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.