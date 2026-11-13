# Issue

**Title:** Document multi-allelic variant filtering behavior

## Description

## Summary
- Add inline comments clarifying that VAF, depth, and alt-depth filters only exclude a multi-allelic variant when **all** ALT alleles fail the threshold
- A variant passes if **any** alt meets the threshold
- No logic changes, documentation only

## Test plan
- [ ] Verify no functional changes by running existing tests

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a085f6b5d3ab`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.