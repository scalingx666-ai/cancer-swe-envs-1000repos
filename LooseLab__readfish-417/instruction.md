# Issue

**Title:** Record unblocked reads in channel_read_latest_decision

## Description

`RUClient.unblock_read_batch` overrides the base method without calling `self.channel_read_latest_decision.update(reads)`, so chunks of an unblocked read that arrive before the unblock takes effect are processed again, even though a decision has already been made.
This  adds the missing call, so it is now matching `stop_receiving_batch`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3da8cf0b452d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.