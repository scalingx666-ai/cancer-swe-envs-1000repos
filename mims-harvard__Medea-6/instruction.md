# Issue

**Title:** fix: get_efo_id returns wrong ontology term, breaking disease target lookup

## Description

## Problem
`get_efo_id` uses the OLS API and blindly returns `docs[0]` — the first
search result regardless of ontology. For common diseases the first result
is not an EFO term:

- "Rheumatoid Arthritis" → `HP:0001370` (HPO phenotype, not EFO/MONDO)
- "Systemic Lupus Erythematosus" → `HP:0002725` (same issue)

`search_disease_efo` then checks `'EFO' in id or 'MONDO' in id`, fails,
retries 5 times, and ultimately returns `None`. MEDEA catches the exception
and continues — producing a confident final hypothesis with no data
grounding. The failure is completely silent to the user.

## Fix
Use the OpenTargets GraphQL search API as the primary lookup. It returns
native EFO IDs directly (e.g. `EFO_0000685` for RA), which
`load_disease_targets` can resolve without issues. OLS is kept as a
fallback but now iterates `docs` to find the first EFO/MONDO term rather
than taking position 0.

## Verified
```python
get_efo_id("Rheumatoid Arthritis")          # EFO_0000685  (was HP:0001370)
get_efo_id("Systemic Lupus Erythematosus")  # MONDO_0007915 (was None)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d7a9c5068bc7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.