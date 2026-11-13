# Issue

**Title:** Cardiac MR: registry/code-prompt wording, slice-major cine layout, hypertrophy chat preset

## Description

## Summary

Registry and code-prompt wording for the cardiac MR node (pairs with the Model Zoo cardiac PR): CardiacMRSegmentation states its inputs (NIfTI or one DICOM series, optional view, LVSA by default) and output (`<node>/voxel_mask/<view>` uint8 label map with class names, pixel spacing and, for cine stacks, the slice-major layout attrs); the code prompt documents the layout so generated scripts reshape to (n_slices, n_frames, rows, cols), pick the end-diastolic frame and measure per slice.

- **Chat preset**: the hypertrophy question adds one line of guidance (measure the maximal end-diastolic LV wall thickness from the short-axis cine segmentation, apply the clinical guideline criterion, report thickness, criterion with source and conclusion). The measurement method and the threshold are left to the agent, which looks the criterion up with web search on.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `4603f1e5e3ae`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.