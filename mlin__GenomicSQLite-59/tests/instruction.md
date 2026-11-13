# Issue

**Title:** Fix edge cases in GRI levels caching

## Description

The levels cache was keyed by the bare table name and validated only by counters that no rollback moves, so it could serve levels that stopped being true: levels computed over writes a rollback later undid, and temp/attached tables' levels filed under the main table's entry.

Unqualified names are now cached only when they resolve to the main database, under a schema-qualified key, compared with SQLite's own identifier comparison. Stores stay autocommit-only, and the cache is bypassed while a writable statement is executing, since trigger-consulted levels reflect its uncommitted snapshot. Eleven regression tests cover the failure modes.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `57baa5517b10`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.