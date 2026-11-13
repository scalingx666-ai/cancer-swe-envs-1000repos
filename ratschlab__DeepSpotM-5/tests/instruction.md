# Issue

**Title:** docs: fix citation metadata and the broken weights-license link

## Description

## Why

`CITATION.cff` never validated against the CFF 1.2.0 schema, so anything that reads it — including GitHub's *Cite this repository* box — had nothing usable. Two violations, found with [`cffconvert`](https://github.com/citation-file-format/cffconvert):

- `year` is not a valid top-level key; the schema expects `date-released`.
- `publisher` must be an entity object, not a string — so `"Cold Spring Harbor Laboratory Press"` was invalid regardless of its content.

Separately, the README's weights-license link 404s, and neither citation file carried the preprint DOI.

## What changed

**`CITATION.cff`** — fixes both schema violations, then adds the metadata citation and archival tooling expects: `version`, `date-released` (from the `v1.0.0` tag), `repository-code`, the DOI under `identifiers`, `keywords`, `abstract`. `license` becomes `PolyForm-Noncommercial-1.0.0` to match `pyproject.toml`; the previous `CC-BY-NC-SA-4.0` is the *weights* license, a separate artifact, now noted in a comment.

**`README.md`**

- `[CC-BY-NC-SA-4.0](WEIGHTS_LICENSE)` → `WEIGHTS_LICENSE.md`. The old target does not exist, so the link 404s.
- Three `medrxiv.org/content/...v1` links → `https://doi.org/10.64898/2026.06.19.26356060`. The version-pinned URLs go stale at v2; the DOI always resolves to the current version.
- BibTeX gains `doi` and `url` — it previously had no persistent identifier. Drops `pages={2026--06}`, a date fragment in a page field that renders as "pp. 2026–06". Publisher corrected to `openRxiv`; the `10.64898` prefix is openRxiv's, not CSHL's `10.1101`. These oddities come from Google Scholar's stale medRxiv template.
- `Raetsch` → `R{\"a}tsch`, matching `CITATION.cff` and Crossref.
- PyPI added to Resources; it was previously reachable only via a badge.

## Verification

- `CITATION.cff` validates against cff-version 1.2.0 (`cffconvert`); APA and BibTeX render correctly.
- All 8 relative links in the README resolve against the working tree.
- Paper metadata cross-checked against Crossref: DOI `10.64898/2026.06.19.26356060`, posted 2026-06-22, publisher openRxiv, author list matches.
- Both changed external URLs return HTTP 200.

No code, packaging or CI changes.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `00ee08d4fa5a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.