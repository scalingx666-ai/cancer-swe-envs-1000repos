# Issue

**Title:** #175 Support for Nextcloud 35

## Description

Fixes: #175 

### Changes
- Declare compatibility with Nextcloud 35 by raising `max-version` from 34 to 35 in `appinfo/info.xml`. The minimum version stays 33.

### Tests

- DICOM Viewer enables, and Files lists the DICOM folders and files.
- Opening the example folder, with 574 images. Chest 3x3 Soft (126 images) renders, and moving one slice changes the instance counter from 1/126 to 2/126.
- Viewer tools work: window/level, zoom, pan, and length.
- A password-protected shared DICOM file opens after the share password is entered.
- No new DICOM Viewer errors appeared in the Nextcloud log during these checks.
<img width="851" height="225" alt="image" src="https://github.com/user-attachments/assets/43ac60f5-2a8b-4b1d-8e97-f471789c11a3" />

### Notes

Reference: https://docs.nextcloud.com/server/35/developer_manual/release_notes/critical_changes.html

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `542fec32e57d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.