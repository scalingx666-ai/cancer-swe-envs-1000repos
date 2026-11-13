# Issue

**Title:** Biostar139647 update to allow selection of a reference in the alignment and creation of insertion

## Description

To answer Issue #227

Biostar139647 update to allow selection of a reference in the clustal alignment.
This allow to include insertions in the output.

### Description
- the user can now select a reference from the aclustal alignment via its label
- this allows to compute insertions in the output sam/bam
- the user can set if heading/trailing gaps should be taken into account, which differenciate short reads VS full genome alignments.
- if no reference label is selected, the previous behavior is kept (no reference in the alignment, only matches and deletions in the sam).

### Checklist
- [X ] Code compiles correctly
- [ ?] All tests passing
- [ X] Extended the README / documentation, if necessary
- [ X] Added myself + history to the source file

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c2e57542f506`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.