# Issue

**Title:** Split `all.yml` workflow triggers into batches of ~10 to avoid GitHub's 50-workflow limit

## Description

`all.yml` directly called 41 reusable workflows and will fail once that count reaches GitHub's 50-workflow-per-run limit as new modules are added.

## Changes

- **`all.yml`** — reduced from 41 individual workflow calls to 4 batch jobs
- **`all_1.yml`** — ci, notebooks, arrayexpress, bigg, biocontainers, biodbnet, biomart, biomodels, chebi, chembl
- **`all_2.yml`** — cog, dbfetch, ena, ensembl, eutils, eva, geo, hgnc, intact_complex, kegg
- **`all_3.yml`** — muscle, mygeneinfo, ncbiblast, omicsdi, omnipath, panther, pathwaycommons, pdb, pdbe, pfam
- **`all_4.yml`** — pride, proteins, pubchem, quickgo, reactome, rhea, seqret, string, unichem, uniprot, wikipathway

Each batch file exposes both `workflow_call` (consumed by `all.yml`) and `workflow_dispatch` (for independent triggering). New modules slot into an existing batch or a new `all_5.yml` — keeping each well under the limit.

<!-- START COPILOT CODING AGENT TIPS -->
---

🔒 GitHub Advanced Security automatically protects Copilot coding agent pull requests. You can protect all pull requests by enabling Advanced Security for your repositories. [Learn more about Advanced Security.](https://gh.io/cca-advanced-security)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6b580e8d9360`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.