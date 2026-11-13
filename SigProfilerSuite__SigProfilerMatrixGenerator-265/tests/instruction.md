# Issue

**Title:** Fix MAF insertion anchor off-by-one in convertMAF

## Description

## Summary

 (and the still-reopened root cause of #209).

`convertMAF()` shifted every MAF indel's `Start_Position` left by 1 before writing it to the simple INDEL format. That shift is correct for deletions, where `Start_Position` is the first deleted base, but wrong for insertions: in GDC/vcf2maf MAFs, an insertion's `Start_Position` is already the anchor base immediately before the inserted sequence (matching the convention `convertVCF()`/`convertTxt()` already use for insertions, with no shift).

Applying the extra `-1` to insertions moves the anchor past the repeat the insertion extends, so most homopolymer insertion counts collapse to a repeat count of 0 instead of their correct value (e.g. `1:Ins:T:0` instead of `1:Ins:T:5`). The issue documents this at scale: 92% of insertions landed in a different ID83 bin across both a 12-project and a 33-project TCGA validation run, cross-checked against an independent ID83 classifier (musicatk).

## Fix

Only apply the `-1` shift when `Reference_Allele != "-"` (deletions). Insertions now use `Start_Position` unshifted.

## Test plan

- [x] Added `test_maf_insertion_anchors_at_start_position`, reproducing the issue's own example (`chr3 52053983` MAF insertion `CTC`) and asserting the corrected anchor.
- [x] Added `test_maf_deletion_still_shifts_by_one`, confirming deletions are unaffected.
- [x] Corrected `test_input_conversion_uses_registered_chromosomes[MAF]`, which previously asserted the buggy (shifted) insertion anchor as expected behavior.
- [x] `tests/scripts/test_input_reference_chromosomes.py` passes locally (12/12).
- [ ] Full suite run blocked locally by an unrelated dataless/iCloud file-sync issue on this machine (`SigProfilerMatrixGenerator/install.py`); CI will validate the full suite.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6bc8e6a5590f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.