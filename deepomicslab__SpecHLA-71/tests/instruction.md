# Issue

**Title:** Fix source builtin error and document conda wrapper commands

## Description

## Summary
- Add `#!/bin/bash` shebang to `script/run.assembly.realign.sh` and `script/ScanIndel/run_scanindel_sample.sh` — both use `source` (a bash builtin) but lacked a shebang, causing `source: not found` errors when invoked with `sh`/`dash`
- Document all conda wrapper commands (`spechla`, `spechla-extract-hla-reads`, `spechla-long-read`, `spechla-assembly`, `spechla-loh`) in the README alongside the existing source script paths

Reported by @wshuai294 in

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `1820c4a58e9c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.