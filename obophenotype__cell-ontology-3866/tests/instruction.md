# Issue

**Title:** Replace leftover temporary ID CL_9900000 with projection neuron CL:0020139

## Description

Fixes task 1 of #3865.

The ID-replacement bot run after #3841 left three references to the temporary ID `CL_9900000` (now `CL:0020139` projection neuron):

- `obsolete CNS long range interneuron` (CL:0000410): `term replaced by` (IAO:0100001) pointed to the non-existent `CL_9900000`.
- CL:0000410: comment text "projection neuron (CL:9900000)".
- `sst chodl GABAergic interneuron` (CL:4023121): comment text "projection neuron (CL:9900000)".

No logical axioms change.

Not touched: `oboInOwl:id "CL:9900000"` annotations on CL:0020032 (oRGC2) and CL:0020075 (hippocampal bistratified interneuron) are older leftovers from earlier PRs, outside the scope of #3865.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8fc8abd63b8f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.