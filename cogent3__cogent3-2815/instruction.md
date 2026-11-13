# Issue

**Title:** DEV: bump version to 2026.11.13

## Description

## Summary by Sourcery

Release version 2026.11.13 with the new metadata API, improved metadata and source propagation, alignment-result fixes, and compatibility deprecations.

New Features:
- Introduce mutable, nested metadata support for sequences, collections, and alignments, replacing the legacy Info model while preserving compatibility for loading older data.
- Add metadata propagation and control across derived collections, serialization, loading, writing, and analysis applications.
- Add metadata-aware warnings for formats that cannot preserve metadata and record alignment parameters for alignment results.

Bug Fixes:
- Correct metadata and source preservation across loading, transformations, and analysis results, including JSON serialization of Smith-Waterman scoring matrices.
- Ensure align_to_ref records its own alignment parameters and no longer reports stale model results.

Enhancements:
- Make source handling explicit and consistent, including support for source-less data and metadata-based writer identifiers.

Build:
- Bump the project version to 2026.11.13 and update the lockfile.

Documentation:
- Document the metadata API, source semantics, serialization compatibility, deprecations, and migration from Info.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6359f2eca133`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.