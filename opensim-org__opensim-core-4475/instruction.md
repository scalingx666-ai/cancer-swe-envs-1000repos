# Issue

**Title:** Add support for mirroring an EllipsoidJoint

## Description

Part 2 of 2 addressing #4481

### Brief summary of changes

Adds the `mirror_axis` property to `EllipsoidJoint`, which mirrors the joint about the plane normal to the given axis ('x', 'y', or 'z') of the parent frame. This is useful for constructing a left-side joint from the description of its right-side counterpart (or vice versa). This leverages recent changes in Simbody for mirroring a `SimTK::MobilizedBody::Ellipsoid` mobilizer (). 

Updating the Simbody commit carried some new other changes that require drive-by fixes:
-  added a `SimTK_NODISCARD` macro for guarding operations that should not discard outputs. Several instances of the vector `normalize()` operation in this repo assumed an in-place operation. These have been fixed, along with an entry to CHANGELOG.md. 
-  introduced initializer list support to SimTK::Vector which broke several constructions using braces (e.g., {}). These have been fixed by instead using parentheses.

### Testing I've completed

Added test case "testMirroredEllipsoidJoint" to `testJoints.cpp`.

### Looking for feedback on...

### AI/LLM use
<!-- Please disclose any AI or LLM tools that were used to create this pull request, how they were used, and what quality checks were performed. -->

Use Claude Code for implementation design iteration and general code review.

### CHANGELOG.md (choose one)

- updated.

Please review the [CONTRIBUTING.md](../CONTRIBUTING.md) file for detailed contributing guidelines.

<!-- Reviewable:start -->
- - -
This change is [<img src="https://reviewable.io/review_button.svg" height="34" align="absmiddle" alt="Reviewable"/>](https://reviewable.io/reviews/opensim-org/opensim-core/4475)
<!-- Reviewable:end -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3bbea8661145`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.