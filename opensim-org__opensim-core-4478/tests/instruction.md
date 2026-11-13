# Issue

**Title:** Improve sample filtering in PolynomialPathFitter

## Description

Part 2 of 3 addressing #4346

### Brief summary of changes

Applies the utilities added in #4477 in `PolynomialPathFitter` to screen the sampled path lengths and moment arms for non-finite values and for outliers, applying a Hampel filter to the samples drawn around each time point. This replaces a comparison against each frame's nominal value that was scaled by the average standard deviation across all frames, which tended to remove many valid samples. 

This change also improves how samples are taken near coordinate bounds by reflecting samples back from the bound into the acceptable range. Previously, many samples were grouped near the coordinate boundary which led unnecessary rejection by the filters.

### Testing I've completed

Added test case "Sampling respects a one-sided coordinate range" to `testPolynomialPathFitter.cpp` to test sample reflection.

### Looking for feedback on...

### AI/LLM use
<!-- Please disclose any AI or LLM tools that were used to create this pull request, how they were used, and what quality checks were performed. -->

Use Claude Code for implementation design iteration and general code review.

### CHANGELOG.md (choose one)

- updated.

Please review the [CONTRIBUTING.md](../CONTRIBUTING.md) file for detailed contributing guidelines.


<!-- Reviewable:start -->
- - -
This change is [<img src="https://reviewable.io/review_button.svg" height="34" align="absmiddle" alt="Reviewable"/>](https://reviewable.io/reviews/opensim-org/opensim-core/4478)
<!-- Reviewable:end -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0b13c2b7333a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.