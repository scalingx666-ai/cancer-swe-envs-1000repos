# Issue

**Title:** fix: escape operator characters in GPR gene ids

## Description

* [x] fix #1448
* [x] description of feature/fix
* [x] tests added/passed
* [x] add an entry to the [next release](../release-notes/next-release.md)

`GPR.from_string` escapes a few characters (`.`, `-`, `:`, ...) before handing the rule to `ast.parse`. Other characters that Python reads as operators or delimiters were not escaped, so a gene id like `a@b` became a `MatMult` node and raised `TypeError: unsupported operation 'MatMult'`. Since `Reaction.copy` rebuilds the GPR from its string, a reaction whose GPR was built from an AST with such ids could not be copied. `#` was worse: `a#b` silently became gene `a`.

This adds escapes for `@ + * % ^ ~ ! ? $ # , ; < > [ ] { }`, the same way as the existing ones. Rules that use only `and`/`or`/`&`/`|` and parentheses parse as before.

Tests: a round trip test for each character and a `Reaction.copy` test for the case in the issue. Both fail on `devel`. `tests/test_core/test_gpr.py`, `test_gene.py`, `test_core_reaction.py`, `tests/test_io` and `tests/test_manipulation` pass locally, and isort/black/flake8 are clean.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6f83a5345695`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.