# Issue

**Title:** Docs: note the -800 HU floor in the density conversion

## Description

Follows #415. Documentation only, no behaviour change, consistent with #378 being closed as wontfix for DiffDRR.

Two additions:

- a docstring on `transform_hu_to_density` describing what the thresholds do, including
  that everything at or below −800 HU is collapsed onto a single value;
- a callout in the `read` docs noting that this removes most aerated lung parenchyma on
  thoracic CT, and pointing users who need it preserved to `nanodrr.hu_to_mu`.

The intent is only to make the convention visible to someone loading a chest CT, since
`transform_hu_to_density` is `exporti` and the behaviour isn't discoverable from the docs
today. 
Happy to reword or trim anything, including dropping the nanodrr pointer if you'd rather not cross-reference packages here.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f12eec1eaa8a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.