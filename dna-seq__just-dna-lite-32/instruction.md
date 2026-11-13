# Issue

**Title:** Fix false-empty module reports

## Description

Root cause: older compiled pharmacogenomics modules had null coordinates despite a valid resolution.csv. Because the sample VCF had no rsIDs, annotation silently matched zero rows.

Changes:
- Require usable chromosome and position coordinates before positional joining in [hf_logic.py (line 222)](/Users/ksuha/src/dna/just-dna-lite/just-dna-pipelines/src/just_dna_pipelines/annotation/hf_logic.py:222).
- Treat unresolved rsID-only modules on ID-less VCFs as “Not assessed,” not an empty biological result.
- Make reports use the current run manifest and ignore stale parquet outputs in [report_logic.py (line 1170)](/Users/ksuha/src/dna/just-dna-lite/just-dna-pipelines/src/just_dna_pipelines/annotation/report_logic.py:1170).
- Display skipped/failed module reasons in the report.
- Recompiled the affected dyshidrotic_eczema_gc_response module with compiler 0.6.1.

Verification:
- Real 4.26M-row sample now matches the expected 5:143399010 G>C, C/C variant once.
- Annotation tests: 51 passed, 3 skipped.
- Report tests: 62 passed, 5 skipped.
- Diff validation passed.
The historical empty HTML was preserved; rerunning annotation will produce the corrected report. The module rebuild only reported non-blocking authoring warnings about renaming sources.csv and closing the completed module spec.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `44382bacf25a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.