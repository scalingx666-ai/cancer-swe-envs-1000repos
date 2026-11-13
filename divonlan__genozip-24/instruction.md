# Issue

**Title:** Fix relative include in arm_crc32_impl

## Description

Hi there, I wanted to try using your software but it won't build for me on arm64. crc32_vec_template.h is being referenced in arm_crc32_impl.h incorrectly. Fixing the path solves the issue on my machine.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `60bf32f06c9a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.