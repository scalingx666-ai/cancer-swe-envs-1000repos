# Issue

**Title:** fix: report the array reference build only when the export declares one

## Description

## What happens today

`_array_reference_build` in `source_intake/detection.py` computes whether the
header declares build 37, and then returns `"GRCh37"` from both branches:

```python
def _array_reference_build(comments: list[str]) -> str:
    joined = "\n".join(comments).lower()
    if any(token in joined for token in _BUILD37_TOKENS):
        return "GRCh37"
    return "GRCh37"  # consumer arrays are GRCh37 unless a future export says otherwise
```

So `SourceDetection.reference_build` reads exactly the same for an AncestryDNA
export that states `human reference build 37.1` in its header and for a file
that states nothing at all. The token scan above it has no effect on the result.

The clearest case is FamilyTreeDNA. Its signature is `forbid_comments=True` —
the absence of a comment block is what distinguishes it from MyHeritage — so an
FTDNA export can never declare a build, and detection has always reported
`GRCh37` for it on an assumption.

## What this changes

`_array_reference_build` returns `None` when nothing was declared. The
assumption is not removed, it moves to the one place that has to pick a build in
order to do coordinate work — where it already lives:

```python
def _effective_array_build(requested: str, declared: str | None) -> str:
    normalized = (requested or "auto").strip()
    if normalized.lower() == "auto":
        return declared or "GRCh37"
    return normalized
```

`declared` is already typed `str | None`, and `SourceDetection.reference_build`
is already `str | None`, so nothing downstream needs to change.

## What does not change

* Every array still parses against the same coordinates. With
  `genome_build="auto"` an undeclared build still resolves to GRCh37, through
  `_effective_array_build`.
* Exports that do declare a build — which is most of them — behave identically.
* `_effective_genome_build` and the sequencing path are untouched.
* No existing test changes.

This follows the repository's own design principle 10, "Tool outputs should be
decisive only when evidence supports that shape", and principle 13's distinction
between a clean empty result and a manufactured one. A build read out of a
header and a build nobody wrote down are different facts, and a host agent
reasoning about liftover or coordinate mismatch can act on the difference.

## Tests

Four tests in `tests/test_source_detection.py`, in a new
`ArrayReferenceBuildTests` class:

* a declared build is reported (AncestryDNA),
* an undeclared one is not asserted (23andMe),
* an FTDNA export reports `None`,
* the intake still resolves `None` to `GRCh37`.

## Verification

* `ruff check src tests` with the pinned `ruff==0.16.2`: clean.
* `python3 -m unittest tests.test_source_detection`: 27 tests, all pass (23
  existing, 4 new).
* `tests.test_genomi_runtime_array_intake`, `tests.test_genomi_runtime_intake`,
  `tests.test_genomi_runtime_provider_detection`,
  `tests.test_parse_source_path_expansion` and
  `tests.test_active_genome_index_downstream_contract`: 30 tests, with 5 errors
  that are identical on `master` before this change and are all
  `ModuleNotFoundError: No module named 'duckdb'` in the `.genome` bundle
  fixture — a missing optional dependency in my environment, not a regression.

## Disclosure

We vendor `source_intake/detection.py` and `source_intake/text_io.py` in our own
project under Apache-2.0, with the licence header, the origin, the pinned commit
and the checksums recorded next to the copy. This is the single behaviour we
changed locally, and it seemed better offered back than kept as a private
divergence. Thank you for the detector — recognising a source by content rather
than by its name is the right shape, and it saved us weeks.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `07a255e5a4fd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.