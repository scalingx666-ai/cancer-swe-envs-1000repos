# Issue

**Title:** Fail clearly when study/population IDs don't match the annotations

## Description

, , . Related: #249, #130, #247.

The most common way `find_enrichment` fails is that the study or population IDs don't match the annotation IDs, for example gene symbols against a GAF's UniProt accessions. When that happened, the run gave little to go on:

- **"No population items" exited with status 0.** It logged `NO POPULATION ITEMS SEEN IN THE ANNOTATIONS` and then called bare `exit()`, so scripts and pipelines saw success. It now exits with status 1, and the message shows the mismatch: `Population IDs (e.g. geneA, geneB, geneC) must match the annotation IDs (e.g. P11, P12, P13); a GAF uses column 2, DB_Object_ID`.
- **The overlap error was hard to act on.** It printed `only 0.39473684210526316 of genes…`. It now reads `only 39% … (--min_overlap 0.7). Study IDs not in the population include: x1, x2, x3`.
- **`Gene2GoReader` with gene IDs passed as `taxids=` (#186)** failed with `NO TAXIDS: gene2go`. It now names the requested taxids and says they are NCBI Taxonomy IDs such as 9606, not gene IDs.
- **`sys.exit` replaces the `site`-module `exit`.**

## Tests
- **New `tests/test_id_mismatch_errors.py`**, added to `CI_TESTS`. It runs the real CLI on tiny files with the small `mini_obo.obo` DAG and checks the exit code and message for both failures, plus the gene2go message. The two CLI tests fail on `main` (exit 0; old message).
- **CI subset:** 201 passed, 12 skipped.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01YaTHwoZmywheAEUdp4zJtb

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0f4999cec94b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.