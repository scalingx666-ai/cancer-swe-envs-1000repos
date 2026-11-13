# Issue

**Title:** fix build failure with Gcc 16

## Description

Starting with Gcc 16, unused but set variables have become error. This results in the following build failure in abyss.

	Consensus.cpp:379:18: error: variable ‘numIgnored’ set but not used [-Werror=unused-but-set-variable=]
	  379 |         unsigned numIgnored = 0;

This change drops occurrences of the numIgnored variable, since it is unused.

Bug-Debian: https://bugs.debian.org/1132058

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a03412ac0fe8`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.