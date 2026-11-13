# Issue

**Title:** Load the full annotated-dataset catalog in the SDRF explorer

## Description

## Summary
- The explorer was still serving a frozen snapshot of a few hundred datasets. It now loads a generated catalog from `bigbio/sdrf-annotated-datasets`: 12,724 accessions and 13,189 SDRF files.
- The catalog file is fetched at page load instead of being embedded in the HTML.
- A weekly workflow rebuilds the catalog, deploys the site, and publishes the `explorer-catalog` snapshot. Ordinary docs builds reuse that snapshot.

## Test plan
- [ ] After the docs workflow deploys, open https://sdrf.quantms.org/sdrf-explorer.html and confirm the header shows about 12,724 accessions.
- [ ] Search for `PXD000070` and open the dataset viewer.
- [ ] Confirm the homepage explorer card shows the same accession count.

Made with [Cursor](https://cursor.com)

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **New Features**
  * The Resources page now displays the annotated dataset count from the latest available catalog data.
  * The Explorer catalog now includes updated dataset metadata and statistics, with more consistent classification of organisms, diseases, experiments, and labels.
* **Improvements**
  * Documentation builds can use a published catalog snapshot, and scheduled updates keep the documentation and Explorer catalog in sync.
  * Catalog summaries are now organized consistently, making dataset information easier to browse.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `03df7bc728dc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.