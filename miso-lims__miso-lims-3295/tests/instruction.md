# Issue

**Title:** #3289: allow entering index sequence alone on bulk library spreadsheet import

## Description

Jira ticket or GitHub issue: #3289
- [x] Includes a change file

## Summary
On bulk library pages, Index 1 / Index 2 cells must match the full dropdown label exactly (e.g. `UDP0001 (GAACTGAGCG)`). Typing or pasting a bare sequence already auto-resolves to the matching label, but spreadsheet import does not: the raw sequence is written straight into the cell and fails validation.

This change lets an index cell contain just the sequence on import. When the cell value is not already a valid label, it is matched against the indices in that row's index family and position; if exactly one index has that exact sequence (case-insensitive), the cell is converted to the full label. No match, or more than one match, leaves the value unchanged (and therefore invalid, as before).

## Details
- Adds a `convertImportValue` column hook in `bulk.js` that, when a column defines it, transforms that column's imported value before it is applied. Only the index columns define it; all other columns are unaffected.
- The index columns (`bulk_library.js`) use the hook to resolve a bare sequence to its label. Because the index family may be supplied in the same spreadsheet, resolution uses the effective (incoming-or-current) family rather than only what is already in the table.
- Scoped to the index columns; other columns are unaffected.
- Matching is **exact** on the index sequence.
- Multi-sequence ("fake sequence") index families are intentionally skipped.

## Testing
Manually tested: imported spreadsheets with bare sequences in Index 1 / Index 2, including the index family supplied in the same spreadsheet; sequences resolve to the correct labels and validate. Also verified full labels still import unchanged, lowercase sequences resolve, and unknown sequences stay invalid.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cbfc0a62ffc4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.