# Issue

**Title:** Add TableUtilities element screening and DataTable::removeRows

## Description

Part 1 of 3 addressing #4346

### Brief summary of changes

Adds methods and utilities for screening elements and removing rows in a `TimeSeriesTable`.
- `TableUtilities::findNonFiniteElements()` detects any NaN or infinite values in a `TimeSeriesTable` and returns the element indexes.
- `TableUtilities::hampel()` implements a Hampel filter than can be applied to the columns of a `TimeSeriesTable` and returns the element indexes of any dected outliers. Added an overload for `TableUtilities::hampel()` that can accept a `SimTK::MatrixView`, which can be useful for apply the Hampel filter to blocks of a `TimeSeriesTable` without requiring any copies. 
- Added `DataTable::removeRows()` for removing several rows of a table (e.g., `TimeSeriesTable`) at once with linear cost. This is opposed to repeated calls to `removeRowAtIndex()` which is quadratic cost since rows must be shifted after each removal. 

### Testing I've completed

Created `testTableUtilities.cpp` with tests for `findNonFiniteElements()` and `hampel()` and added tests to `testDataTable.cpp` for `removeRows()`.

### AI/LLM use
<!-- Please disclose any AI or LLM tools that were used to create this pull request, how they were used, and what quality checks were performed. -->

Use Claude Code for implementation design iteration and general code review.

### CHANGELOG.md (choose one)

- updated.

Please review the [CONTRIBUTING.md](../CONTRIBUTING.md) file for detailed contributing guidelines.

<!-- Reviewable:start -->
- - -
This change is [<img src="https://reviewable.io/review_button.svg" height="34" align="absmiddle" alt="Reviewable"/>](https://reviewable.io/reviews/opensim-org/opensim-core/4477)
<!-- Reviewable:end -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `01683ac33568`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.