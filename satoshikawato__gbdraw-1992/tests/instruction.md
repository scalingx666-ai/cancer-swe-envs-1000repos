# Issue

**Title:** Say the Clear LOSAT count is the project's, and keep Linear draft comparisons and Session 39 ring codes

## Description

The Web's **Clear LOSAT results** button now says that its count is the project's ("Clear the project's 3 LOSAT results"), because it clears the LOSAT results of every drawing, not only those of the shown drawing. Two Web fixes come with it: rotating a Linear record to a feature, Align, or Align at a feature no longer writes the comparisons of the last Generate into the drawing's settings (OV-3314), and a Session 31–39 whose LOSAT rings were moved after its last Generate now opens with each ring's own genetic code instead of the codes swapped (OV-3179).

## Change class

Select exactly one:

- [x] STANDARD
- [ ] GOVERNANCE
- [ ] ARCHITECTURE_EXCEPTION
- [ ] PROMOTION

## Purpose

- Applicable baseline: `dev` at `df85b4a30`; the trusted CI profile of a Web runtime change; focused owners: `adoptCanonicalRenderArtifacts` and `restoreStoredNonCanonicalConfig` in `gbdraw/web/js/services/config.js`, the Clear buttons in `gbdraw/web/index.html`.
- The wording follows the Owner's answer of 2026-11-10 to the per-drawing Clear question (option A): Clear stays a whole-project clear (PD-OI-022 unchanged) and its label says the count is the project's.

## User-visible impact

- **Clear LOSAT results** (Circular and Linear panels): with results, the button reads "Clear the project's N LOSAT result(s)" instead of "Clear N LOSAT result(s)". With none it still reads "Clear LOSAT results", and the hints are unchanged. The new English keys are not translated yet; the other languages show the English until the pre-tag translation batch, as `node tools/i18n/sync.mjs status` lists them.
- Linear: after Rotate record to feature, Align, or Align at a feature, the drawing's settings keep the comparisons they held (for example the empty list of a loaded Session whose saved comparisons wait for Inherit or Replace). The figure the rerender draws is unchanged; the next Generate uses the settings as the user left them. Circular rings already work this way.
- Session 31–39 Load: each LOSAT ring opens with its own genetic code when the rings were moved after the last Generate.

Before (dev) and after, the same project (two Circular drawings; the shown one has one LOSAT ring, the project three searches), Circular **Pairwise Comparisons** panel at the default Settings width:

| Before | After |
| --- | --- |
| ![before](https://raw.githubusercontent.com/satoshikawato/gbdraw/pr-screenshots/pr/cmf-followup-clear-rerender/clear-losat-before.png) | ![after](https://raw.githubusercontent.com/satoshikawato/gbdraw/pr-screenshots/pr/cmf-followup-clear-rerender/clear-losat-after.png) |

## Changes

- `gbdraw/web/index.html`: both Clear buttons use the keys "Clear the project's {count} LOSAT result" / "... results" (one wording, two panels).
- `gbdraw/web/js/services/config.js`:
  - `adoptCanonicalRenderArtifacts`: the Linear branch that binds the request's comparisons into the drawing's inputs runs only for a Generate's own adoption, not for a candidate of the committed request (`conservationPairs: 'committed'`).
  - `restoreStoredNonCanonicalConfig` (Session 31–39 Load): each projected ring takes `losat_gencode` from the stored draft entry that `conservationSourcesOfSeries` pairs with that ring's table, instead of the entry at the same index; `readDraftOverCommittedRequest` passes the projection's ring tables.
- `tests/web/session-losat-cache-validation.test.mjs`: a committed adoption leaves the draft's comparisons empty (OV-3314); two Session 39 cases built from `whitelist-tab-keyword.v39` with two TLOSATX rings in the shape the `main` `cdd31013` Web writer gave them load each ring's own code (OV-3179): rings moved after the Generate (the matcher pairs them by table name), and rings moved and then a genome added with Add comparison sequence (each entry then carries its genome's name, so the stored place decides).
- `tests/web/run-analysis-simple-path.test.mjs`: the template pin reads the new keys in both panels.
- `changelog.d/fix-cmf-followup-clear-rerender.md`.

## Verification

- Failing first on `df85b4a30`'s `config.js`: the OV-3314 case fails (the committed adoption filled the draft with the four committed comparisons). With the by-index pairing restored in a copy outside the worktree, both Session 39 cases fail (Ring A code 4, Ring B code 11). With the matcher's place pass turned off in such a copy, only the Add comparison sequence case fails, so that case pins the place pass.
- `node --test` on `session-losat-cache-validation`, `load-repair-dialog` (every Session fixture loads), `stored-record-id-places`, `run-analysis-simple-path`, `history-canonical-owner`, `ring-draft-transitions`, `circular-rings-setting`: all pass.
- `i18n-catalogs` and `i18n-tools` pass (missing and stale keys are allowed before the release tier).
- Guards: `typed-boundaries` (tsc), `explicit-any-ratchet`, `function-size-ratchet`, `owner-graph-baseline`, `error-producer-coverage`: pass.
- Browser: the screenshots above, from one Playwright run per side; the Circular button keeps one line (34 px high, text fits its 286 px row).

## Risk and review notes

- Gate result and any blocker: none known.
- Review result and why it is `CLEAR` or `REQUIRED`: `CLEAR`; no Product Contract or guard change.
- Architecture impact: **This is not architecture-bearing**. No owner or path is added; one writer path (a committed rerender into the Linear draft) and one index pairing are removed.
- Architecture baseline and changed-scope conclusion, if architecture-bearing: N/A
- `architecture-change` label, if relevant: N/A
- Persisted contract: N/A (no writer change; the Session 31–39 reader pairs rings by the existing matcher).

### Boundary analysis

- Channel (Clear wording): the count is `clearableLosatResultCount` (`app/run-analysis.js`, the project's LOSAT cache size); the two template expressions in `index.html` read it. Only the text keys change.
- Channel (OV-3314): the writer of a Linear drawing's draft comparisons (`files.linearCanonicalComparisons`) is `bindDrawingCanonicalComparisons` (`services/drawing/inputs.js`), called by `adoptCanonicalRenderArtifacts` for every adoption. Readers: the next Generate's request and Save. A rerender of the committed request (`runCommittedCanonicalCandidateInternal`: Rotate record to feature, Align, Align at feature) adopts with `conservationPairs: 'committed'`; the label reflow commits through `commitLiveSettingValues` and never bound the Linear comparisons. Rule applied: a rerender of the committed Session commits only to the committed Session and leaves the draft (R1 (c)), the same rule the Circular rings follow. Removed: the committed-rerender write. Generate's adoption and the Load paths (which bind through their own calls) still bind.
- Channel (OV-3179): the Session 31–39 first pass (`readDraftOverCommittedRequest`) writes each projected ring's `losat_gencode` from the stored draft; the key was the series index. Rule applied: find a ring by its identity through the one matcher (`conservationSourcesOfSeries`: source key, file name, stored place) instead of by position. Removed: the by-index pairing. No second matcher.
- Twins left: none added.
- Remaining work: the Clear keys in the locale catalogs (pre-tag translation batch).

## Rollback

Revert the merge commit.

## Conditional Product Impact

- Product-impact role: N/A
- Product preflight classification: N/A
- Affected concern(s), if known:
- Affected journey/checkpoint effects:
- Authority and decision references: Owner answer 2026-11-10 (Clear stays a whole-project clear; the wording says the count is the project's).
- Decision Pack or evidence reference, if required:
- Behavior contracts and residual risk:

<!-- gbdraw-product-impact-decision:start -->
{"schemaVersion":1,"headSha":"","decisions":[]}
<!-- gbdraw-product-impact-decision:end -->

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c04bada2e6b7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.