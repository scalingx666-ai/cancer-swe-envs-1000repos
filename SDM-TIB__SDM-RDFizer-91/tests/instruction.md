# Issue

**Title:** rdfizer: import psycopg2

## Description

PostgreSQL is broken in 4.6.2 because the PostgreSQL client library is not imported.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8e0fa251b79f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.