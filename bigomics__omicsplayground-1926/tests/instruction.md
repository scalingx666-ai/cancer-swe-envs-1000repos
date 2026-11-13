# Issue

**Title:** disable ellipsis in table

## Description

**Problem:**
Geneset links to external sources disappeared becauses of 'ellipsis' use in datatable.

**Fix:**  Ellipsis disabled.

**Before:**
<img width="1105" height="396" alt="image" src="https://github.com/user-attachments/assets/ef2cda9e-a136-4d44-acf5-2b0f52fec9e0" />

**After:**
<img width="1105" height="396" alt="image" src="https://github.com/user-attachments/assets/d8c38898-dd48-42ef-bcef-09cbd1fa4e8c" />

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Updates**
  * The gene-set column in the enrichment analysis table no longer uses ellipsis formatting. Long gene-set names may appear differently in the table, while the existing server-side shortening remains unchanged.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8e21a39e948b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.