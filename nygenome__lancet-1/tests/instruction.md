# Issue

**Title:** Fix compilation with Clang

## Description

Add `#include <vector>` in each .cc/.hh pair that uses `std::vector`.

Previously VariantDB.cc compilation failed for me with Clang — presumably with the GCC version you've been using some other C++ header happens to include `<vector>` as a byproduct, thus hiding this problem.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e628b15823d8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.