# Issue

**Title:** BAM Parser Performance Tweaks

## Description

Benchmarking .NET Core vs. Mono (http://evolvedmicrobe.com/blogs/?p=398) showed a few quick areas that could be fixed, which I implemented after writing the post.

The easiest performance win available would now would likely be to avoid copying the `byte[]` array  when creating the sequence type, and just reuse the one used by the parser.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5fe52bfc4fa9`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.