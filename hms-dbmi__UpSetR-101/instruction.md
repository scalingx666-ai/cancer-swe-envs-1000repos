# Issue

**Title:** Refactor plotting code

## Description

This PR allows the user to include or omit the grid.newpage calls in the upset as they desire. It also allows the user to save an upset object for later printing. This is accomplished by a minimal class definition and the addition of an argument which controls the grid calls.

This addresses issue #90, and is a similar solution to #82

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ebf4ee08ef90`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.