# Issue

**Title:** Separated minimums between design and simulate

## Description

## Changes in this PR

The minimum primer length is set at 15, which is probably reasonable for designing new primers but is too restrictive for simulating given primers. The cited reference in code comment supports using 7, instead of 15. 


This changes there to be a minimum for design (15, as existing code uses) and for simulate (7, as cited in paper). I also added an error for passing in short primers.

### Why are you making these changes?
I would like to use simulate to test my own primers, but index errors are thrown if I use primers smaller than minimalPrimerLength

### Are any changes breaking? (IMPORTANT)
The design code is unchanged. The simulate behavior changes because if someone simulated with short primers, the code would previously blow up with index error.

## Pre-merge checklist
*All of these must be satisfied before this PR is considered
ready for merging. Mergeable PRs will be prioritized for review.*

I actually do not see what linter is used (I've not written Go code before) - so please let me know what is appropriate here! Thanks!

* [x] New packages/exported functions have docstrings.
* [x] New/changed functionality is thoroughly tested.
* [x] New/changed functionality has a function giving an example of its usage in the associated test file. See `primers/primers_test.go` for what this might look like.
* [x] Changes are documented in `CHANGELOG.md` in the `[Unreleased]` section.
* [ ] All code is properly formatted and linted.
* [x] The PR template is filled out.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `529ccc7d9671`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.