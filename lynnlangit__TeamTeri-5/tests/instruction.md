# Issue

**Title:** cleanup

## Description

renamed:    1_GCE-standup.sh -> 1a_gce-standup.sh
renamed:    3_GCE-standup-boot-script.sh -> 1b_gce-standup_and_run_boot-script.sh
renamed:    2_GCE-cli-cleanup.sh -> 2_gce-cleanup.sh

changed: the reference to cli.rc within these files
changed: formattimg the line that launches the instances

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3f8b294940f6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.