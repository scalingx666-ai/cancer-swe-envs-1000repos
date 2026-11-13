# Issue

**Title:** Fixing a few things that got lost in the transition to github

## Description

Somaticspike.xml didn't make it through the initial transition, so here it is again.  It probably needs to be updated to include the public key, but for now at least it's here again.

Benchmarking scripts expect LibraryFilterRead to exist, so I'm putting it back.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9205157686d2`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.