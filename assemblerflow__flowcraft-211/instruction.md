# Issue

**Title:** Set phred encoding when it fails to be determined - trimmomatic

## Description

Currently, the trimmomatic module fails when the phred encoding is unable to be determined. This can be avoided if the encoding is set to phred33 in these cases. I've tested with a few samples and it works well. It's also what is done in the INNUca pipeline.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c8a85748098a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.