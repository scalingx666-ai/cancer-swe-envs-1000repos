# Issue

**Title:** Test the RTStruct merger, and fix what that uncovered

## Description

> Stacked on #181 (→ #180 → #179).

`RTStructMerger` had no tests. Writing them found two defects.

## Duplicate ROI names raised

```python
struct_set_roi_seq += "_2"
```

That adds a string to a `Dataset` rather than to its `ROIName`:

```
TypeError: unsupported operand type(s) for +=: 'Dataset' and 'str'
```

So merging two structure sets that both contain a `Liver` — the ordinary case, since two sets for one series routinely name the same organ the same way — was impossible. **The rename path had never run successfully.**

Suffixes now count upward until one is free, so merging a third set gives `liver_3` rather than a second `liver_2`.

## Renumbering could collide

It counted the destination sequence rather than taking the highest number in use. With a gap — from an ROI deleted elsewhere, which `delete_roi` in #180 now makes easy to create — that hands out a number another ROI still holds. `ROINumber` is the key joining `StructureSetROISequence`, `ROIContourSequence` and `RTROIObservationsSequence`, so two ROIs sharing one would silently share contours.

This mirrors the fix already made in `RTStruct._next_roi_number`.

## Tests

Nine, covering what a merge has to *preserve* rather than merely that it returns:

- every ROI from both sets is present;
- **each one's geometry is unchanged** — names alone would pass even if contours were attached to the wrong structure;
- `ROINumber`s stay unique;
- the three sequences stay in step;
- no contour references an ROI that does not exist;
- the result survives a save and reload.

Three of the nine fail without the fixes above.

.

226 tests pass, under pydicom 3.0.1 and 2.4.5.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bc07d7dec4ee`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.