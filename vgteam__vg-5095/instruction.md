# Issue

**Title:** add "refpos" field to `vg filter --tsv-out`

## Description

## Changelog Entry
To be copied to the [draft changelog](https://github.com/vgteam/vg/wiki/Draft-Changelog) by merger:

 * `refpos` field option added to `vg filter --tsv-out`

## Description

Expose yet another thing to `--tsv-out`, this one because it's common to want a vague understanding of where an alignment belongs to. Only prints the first refpos field in case of a multi position annotation. I pinged an intended user to ask if that is enough.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a0907af0ad0e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.