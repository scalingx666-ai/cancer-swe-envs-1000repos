# Issue

**Title:** Add close worker function

## Description

Sorry for the multiple PRs!

I want to dynamically create Aioli workers based on some user interactions, however, once I'm done with the worker I can't find a way to terminated them? Maybe I'm missing something, but in this PR I've added `close()` to the exposed functions so that workers can be shutdown from the main thread.

-W

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4e85963becf3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.