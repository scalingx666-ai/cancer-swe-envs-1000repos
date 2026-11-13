# Issue

**Title:** updated devcontainer image.

## Description

## Changes in this PR

Updating the devcontainer to use go 1.23 and debian 12 `bookworm`.


### Why are you making these changes?

Originally wanted to use a smaller dev container for faster builds but the official Go devcontainer images don't support alpine?

### Are any changes breaking? (IMPORTANT)

No. It builds and all tests pass within the build.

## Pre-merge checklist
*All of these must be satisfied before this PR is considered
ready for merging. Mergeable PRs will be prioritized for review.*

* [X] New/changed functionality is thoroughly tested.
* [X] All code is properly formatted and linted.
* [X] The PR template is filled out.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9b7d07ce5b4d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.