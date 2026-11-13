# Issue

**Title:** docs: 2.82.0 release summary in NEWS

## Description

Adds a curated **GEOquery 2.82.0** section at the top of NEWS.md summarizing user-facing changes since 2.80.0 (Bioconductor 3.23): breaking changes, new features, deprecations, bug fixes and docs. The 2.81.x entries stay below as the detailed changelog. Internal and test-only items are left out of the summary.

- Resolves a contradiction between NEWS entries: the 2.81.21 entry says `returnType` "remains ExpressionSet" by default, but the code (and the Breaking note) default to `SummarizedExperiment`. The summary follows the code.
- Fixes the `DESCRIPTION` `Description:` field, which still said Series Matrix files parse to `ExpressionSet` by default.
- Bumped to 2.81.36. **Merge after #236** (2.81.35); the summary already includes the #235 fix.

`DESCRIPTION` stays at 2.81.x; Bioconductor sets 2.82.0 when it branches the release. The new NEWS parses and formats with `tools:::.build_news_db_from_package_NEWS_md()`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `22c6cab9a48f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.