# Issue

**Title:** Add DIAMOND, Infernal

## Description

This PR adds diamond and infernal, with SIMD support for diamond (infernal doesn't seem to benefit much from WebAssembly SIMD in some quick tests on cmsearch and cmcalibrate)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `da8e1c029761`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.