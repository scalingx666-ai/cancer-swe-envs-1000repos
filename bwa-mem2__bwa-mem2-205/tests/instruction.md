# Issue

**Title:** GCC 11 now defines __rdtsc so make definition test conditional on GCC version

## Description

As far as I can tell GCC 11 (used in Ubuntu Jammy and later) now defines __rdtsc in it's intrinsics. Therefore util.h definition of this should be conditional on gcc version. Feel free to make the version check more specific if you see the need.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `edc703f883e8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.