# Issue

**Title:** Check legacy protein references without copying the drawing's features

## Description

A Generate that loads an older Session checks that every legacy protein reference (`p_r_...`) in its orthogroups, features and selected alignment feature resolves through the current protein identity. Until now `app/run-analysis.js` did this by building rewritten deep copies of the orthogroups and both feature lists and then searching the copies; nothing used those copies. This PR makes the check read the values in place and keeps the same answer (one exception below), and adds the missing History step to the OV-3352 journey: going back to a Generate that migrated legacy protein caches restores the feature catalog's own objects and its orthogroups.

## Change class

- [x] STANDARD
- [ ] GOVERNANCE
- [ ] ARCHITECTURE_EXCEPTION
- [ ] PROMOTION

## Purpose

- Applicable baseline: `dev` at `df85b4a30`; focused owners: the pre-run legacy protein reference check in `gbdraw/web/js/app/run-analysis.js`, `tests/web/run-analysis-simple-path.test.mjs`, and the OV-3352 case in `tests/web/history-rule-preparation.playwright.spec.js`.
-  (OV-3352): that PR stopped the commit of a migrating Generate from copying the features, but the pre-run check still built copies only to inspect them.

## User-visible impact

None for any Session gbdraw writes. The check accepts and refuses the same inputs with the same messages, with one exception that only a hand-edited Session can reach: an object with its own `__proto__` key. The old copy turned that entry into a prototype assignment and never searched it, so a legacy reference under it was accepted; the check now refuses it like any other reference left after mapping. A Generate of an older Session with legacy protein references no longer builds two copies of the orthogroups and feature lists before it starts.

## Changes

- `gbdraw/web/js/app/run-analysis.js`: `rewriteMappedProteinReferences` (a deep-copying rewrite) is removed. `requireLegacyProteinReferencesMigrate` walks the values once without copying them and throws the two refusals the rewrite and the follow-up search threw: a map that turns an object key into another key of the same object, and a legacy reference left after mapping. `mappedProteinReferenceText` is the one mapping of a text; the check uses it, and so does the only installed value, the selected alignment feature (a string, which the Generate installs after the run).
- `tests/web/run-analysis-simple-path.test.mjs`: a case pins the check's answer for nine inputs (acceptance, both refusals, their order, a map that is not an object, a key that holds a reference inside other text) and that the check leaves the values unchanged.
- `tests/web/history-rule-preparation.playwright.spec.js`: the OV-3352 journey reads the installed state through one helper (`migratedFeatureState`, which now also checks `biologicalFeatures`), and ends with the step "OV-3352: going back in History to the migrating Generate keeps its features": after the rule edits and the parity Generate, the History list walks back to the migrating Generate's step and the state must equal the state right after that Generate, with the catalog's own feature objects. The fixture selects no alignment feature, so this step does not exercise the mapping of a selected one; that mapping is the same `mappedProteinReferenceText` call, checked by the script below.

## Verification

- The node case fails on the base (`requireLegacyProteinReferencesMigrate is not a function`) and passes on the head. With the duplicate-key test disabled in the check it fails again.
- Same answers as before: a script ran the base `rewriteMappedProteinReferences` plus the base search, and the new check, over the same ten inputs (the nine above plus a whole selected text). All ten answers, and the selected alignment feature each produced, were identical. The review added inputs (shared sub-objects, cycles, numbers, booleans, `undefined`, `NaN`, sparse arrays, a `constructor` text): identical; only the three `__proto__` inputs differ, as described under User-visible impact.
- Playwright, `--workers=1`, only the OV-3352 case: passes on the head (1.3 min). With the old deep copy put back in the migrating Generate's commit (and the two earlier checks of the case made non-fatal so the run reaches the new step), the new step fails: `catalogFeaturesInstalled` is `false` after going back to that Generate.
- A probe found that an Undo of a later feature edit restores the catalog's objects even when the Generate installed copies, so the step goes back to the Generate's own History step instead.
- Node guards: `typed-boundaries`, `explicit-any-ratchet`, `function-size-ratchet`, `owner-graph-baseline`, `architecture-contracts`, `drawing-slices`, `feature-visibility-rule-writers`, plus `run-analysis-simple-path`, `run-analysis-derived-cache`, `losat-cache`, `protein-losat-cache-keys`: 284 pass, 0 fail.

## Boundary analysis

- Channel: the Python helper `resolve_legacy_protein_reference_map_json` writes the reference map; the pre-run block of `createRunAnalysis` reads it with this Generate's working orthogroups, features and selected alignment feature. Only the selected alignment feature leaves that block (`selectedOrthogroupAlignmentFeature`); the orthogroups and features of the Generate come from its own catalog and results.
- One owner per transformation: the mapping of a text has one function, used by the check and by the installed value. The check reads and does not build a second form of the data.
- Removed: `rewriteMappedProteinReferences` and the three discarded copies.
- Twin left: none. Remaining work: none for this check.

## Risk and review notes

- Gate result and any blocker: `node tools/check-web-change-budget.mjs --base origin/dev --head HEAD`: Gate PASS, ordinary profile, size CLEAR.
- Review result: `REQUIRED` for the inventories it lists: one new export from `app/run-analysis.js` (`requireLegacyProteinReferencesMigrate`, exported for the node case) and the compatibility-like names it carries (`Legacy`), which describe the same existing older-Session check.
- Architecture impact: **This is not architecture-bearing**; the check stays in the same owner and path.
- `architecture-change` label: not needed.
- Persisted contract: `N/A`.
- Decisions taken alone, each Owner-delegated (standing instruction 2026-09-29, restated 2026-10-07):
  - The selected alignment feature is still mapped, because the Generate installs it. Rejected: drop every rewrite, which would install the legacy text for a Session whose selected alignment feature holds a legacy reference.
  - The History step goes back to the migrating Generate's own step at the end of the journey. Rejected: the Undo of a later feature edit (it restores the catalog's objects even when the Generate installed copies, so it cannot fail), and a step before the rule edits (it would restore the catalog's objects before the rule check and hide the case's own failure).
- A follow-up in the same list (one value for a blank number field) is not in this PR; its analysis is in the task handoff.

## Rollback

Revert the PR. Nothing is persisted.

## Conditional Product Impact

- Product-impact role: N/A
- Product preflight classification: N/A
- Affected concern(s), if known:
- Affected journey/checkpoint effects:
- Authority and decision references:
- Decision Pack or evidence reference, if required:
- Behavior contracts and residual risk:

<!-- gbdraw-product-impact-decision:start -->
{"schemaVersion":1,"headSha":"","decisions":[]}
<!-- gbdraw-product-impact-decision:end -->

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7197ba5e7163`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.