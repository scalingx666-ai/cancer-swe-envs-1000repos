# Issue

**Title:** Drop hd5write.default import

## Description

This function is not exported by rhdf5 anymore in favour of the corresponding S3 method.
While sleuth already does not use `hd5write.default` anywhere (anymore?), it still imports it, breaking the installation on up-to-date systems.
This PR fixes this by dropping the unnecessary import statement.


Also see

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e5ac761e999a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.