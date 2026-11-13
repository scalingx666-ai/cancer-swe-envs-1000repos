# Issue

**Title:** [batch,ci] dedicated driver to CI callbacks

## Description

## Change Description

Remove the generic callback feature altogether, replacing it with a dedicated nudge from the batch driver to CI on a new, purpose built endpoint.

## Security Assessment

- This change potentially impacts the Hail Batch instance as deployed by Broad Institute in GCP

### Impact Rating

- This change has a high security impact

### Impact Description

Reduces the potential attack surface of a feature that has only one actual use case.

### Appsec Review

- [x] Required: The impact has been assessed and approved by appsec

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `12571d49651f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.