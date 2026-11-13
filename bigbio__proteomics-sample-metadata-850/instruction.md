# Issue

**Title:** Sync sdrf-templates (NPQ, MS scan-range IDs); update TERMS.tsv

## Description

## Summary
- **sdrf-templates submodule** a9cb494 → 0551c79 (bigbio/sdrf-templates main). This brings in:
  - bigbio/sdrf-templates#74: NPQ (NULISA Protein Quantification) allowed in `comment[quantification unit]`; NULISA examples in affinity-proteomics.
  - bigbio/sdrf-templates#75: MS scan-range and min/max MZ columns moved to PRIDE:0001029–0001035; ms-proteomics 1.2.0 (unreleased) folded into 1.1.0.
- **TERMS.tsv**:
  - rows `ms1/ms2/ms3 scan range` and `ms2/ms3 min/max mz` now use PRIDE:0001029–0001035. The old IDs PRIDE:0001008–0001014 belong to other released terms; for example, PRIDE:0001009 is "soil type method".
  - `quantification unit` values are now `NPX, RFU, NPQ`, matching the template.

## Dependency
The new PRIDE IDs are added by PRIDE-Archive/pride-ontology#212 (merged into `dev`). They resolve in OLS once that release reaches `master` and OLS reloads.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Chores**
  * Updated the SDRF proteomics templates to a newer revision. The available change details do not identify specific template updates or describe changes to user-facing functionality, so no further impact can be confirmed.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dc9be283dd1d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.