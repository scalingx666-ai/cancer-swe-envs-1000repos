# Issue

**Title:** Move NIfTI cohorts to Aspera and demonstrate public CT segmentations

## Description

The main TCIA queries workshop now ends with an open-access NSCLC-Radiomics CT/DICOM SEG sample, selected within the same participant and study and bounded at two series. The brain MR/NIfTI cohort and geometry lesson moves to the existing Aspera notebook, which accepts a saved participant cohort or a Participant Explorer packageUrl,packagePath CSV. Aspera installation and invocation stay in that notebook.

The setup pins ascli 4.28.0 for the public file-list fixes. The package uses tcia_utils 4.0.0a17 and its metadata-only cohort export; merge after that preview is on PyPI. Existing-file reuse instructions no longer require resume.

Validation: 35 notebook/adapter tests; deterministic notebook generation; both workflows against live public metadata and then recorded fixtures using the installed SDK wheel. The Aspera example exported two of 70 indexed files for two participants. All image transfers were blocked or intercepted. Ruby/Aspera installation and real Aspera payload transfer were not exercised. No server or artifact update is required.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7adf5b51d8ed`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.