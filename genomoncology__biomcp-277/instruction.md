# Issue

**Title:** Ticket 1194: the final load tier

## Description

Three residual saturation-sensitive spots closed: the disease bounded-runner observation windows widened to 60s with the post-kill ready requirement correctly dropped; the drug-card and GenCC-parity spec blocks get Mustmatch timeout=600. No assertion changed meaning; production untouched. Review ACCEPT with label corrections applied; saturated proofs: disease 1/1 in 3.21s, drug 15/15, gene 22/22, all under 12 spinners. Parent runs the merged saturated gate.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fc81e388021e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.