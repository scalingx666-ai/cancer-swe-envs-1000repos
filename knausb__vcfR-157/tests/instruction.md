# Issue

**Title:** dplyr 1.0.0 fixes

## Description

`ifelse()` returns a logical vector if the Type is length 1; `if_else()` returns a character vector. dplyr 1.0.0 is stricter about combining types so this becomes an error. This shouldn't affect vcfR with the CRAN version of dplyr.

I had to guess at the value of the third argument; you should double check it.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f018f634895c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.