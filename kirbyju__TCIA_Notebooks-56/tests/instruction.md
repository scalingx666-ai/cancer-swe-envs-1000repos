# Issue

**Title:** Explain sample reuse and controlled-file summary counters

## Description

The workshop now recommends retaining the destination and removing max_items after inspecting a sample. It explains that resume=True is optional for normal reuse, public DICOM sync jobs can fetch missing files, and RC2 can count existing controlled files as Downloaded with Synced: 0.

The controlled-download section also explains why standalone manifests can use a generic manifest folder and preserve ZIP filenames instead of the public DICOM hierarchy. ZIP files from this route remain archives.

Validation: 20 notebook checks passed and the notebook regenerated successfully. All code cells are unchanged. The corresponding SDK guidance is updated in kirbyju/tcia_utils#56. A released-binary test using synthetic localhost files confirmed existing payloads were reused despite the Downloaded counter. No TCIA payloads or controlled credentials were used.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d654af8e3266`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.