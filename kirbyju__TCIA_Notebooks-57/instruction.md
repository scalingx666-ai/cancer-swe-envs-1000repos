# Issue

**Title:** Distinguish DICOM-series sizes from controlled ZIP download bytes

## Description

The controlled CT/SEG example now distinguishes reported DICOM-series sizes from exact ZIP payload bytes. It displays the size basis and published archive-size label, and keeps unknown exact byte counts distinct from zero. The notebook installs tcia_utils 4.0.0a15, which fixes the incorrect size assertion while retaining explicit size and checksum validation.

The selected CT/SEG identities, download call, destination and approved-key requirements are unchanged. Shared API source in kirbyju/tcia-query-skill#17 is deployed as 0.7.1 and verified through REST/MCP without rebuilding bundles. The fixture contains actual hosted responses from that deployment.

Validation: 20 notebook checks; full offline and public-metadata live execution with the built hotfix wheel; and full replay with the exact hash-verified PyPI wheel. All image transfers were blocked. The published SDK also passes 15 size regression tests without pandas and correctly prepares the two reported public metadata records. Synthetic ZIP checks with released TDR still reject deliberately wrong exact sizes/checksums. No controlled payloads or user credentials were used.

Version 4.0.0a15 is published on PyPI and GitHub as a preview. The source API and Python fix are ready for this notebook merge.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5d6386247c69`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.