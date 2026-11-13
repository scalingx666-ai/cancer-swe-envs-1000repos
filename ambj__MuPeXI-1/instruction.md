# Issue

**Title:** Replace call to pandas's deprecated method

## Description

The method pandas.DataFrame.sort_values replaced pandas.DataFrame.sort from pandas's version 0.17.0, and the call to the deprecated method was causing a bug preventing the writing of MuPeXI output files in environment with up-to-date versions of pandas (bug observed with pandas 0.20.1 but not with pandas 0.18.1).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2bc5da0b3b87`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.