# Issue

**Title:** Exit 0 on -h/--help in C programs

## Description

The usage block in every program ended with "return 1", so asking for help looked like a failure. --help was not registered as a long option anywhere (it fell through as an unknown option), and hmm_flagger and depth2cov did not accept -h at all.

- Return 0 from the usage block when -h/--help was given; unknown options still return 1.
- Register --help in every program; programs using plain getopt switch to getopt_long with a help-only option table.
- Add 'h' to the optstrings of hmm_flagger and depth2cov.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5d59e5e20b46`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.