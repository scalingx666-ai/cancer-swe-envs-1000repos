# Issue

**Title:** Ticket 1197: the docs-verifier window closes

## Description

The last load-sensitive test in the repo: two fail-closed security probes ran a 0.01s real-clock budget that extreme starvation could exhaust before first admission. A seven-line frozen-clock injection at exactly those two calls; no assertion touched; verifier script untouched. Review ACCEPT. Proven on both hosts under the exact failure conditions: 3/3 and 8/8 on the gate host with 12 spinners; passes under 48 spinners on the dev host.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b80c1730ab99`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.