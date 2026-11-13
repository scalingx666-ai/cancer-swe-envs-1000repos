# Issue

**Title:** Fix Empty Subjects in MySQL

## Description

This PR fixes an issue when the source to be semantified is a MySQL database and the column used in the subjectMap includes NULL values. No triples are (to be) generated in that case.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `53387767bded`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.