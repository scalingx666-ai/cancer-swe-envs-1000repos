# Issue

**Title:** Add primer pair analysis and selectable Tm

## Description

## Summary

Add an opt-in Benchling-compatible SantaLucia Tm profile and a read-only endpoint that evaluates complete PCR primer pairs.

- Apply the selected Tm profile consistently to single-primer checks, degenerate Tm ranges, and cloning or generic primer design while preserving the Primer3 default.
- Add `check-primer-pair`, which checks explicit 3' annealing arms against the template and evaluates hairpins, homodimers, and heterodimers on the complete tailed oligos.
- Report candidate amplicons, capped-search status, and dU-to-T normalization. Keep PCR product enumeration in the cloning layer while preserving the existing hub re-export.

## Verification

- `uv run pytest -q tests/test_primer_check.py tests/test_agent_api.py::TestCheckPrimer tests/test_agent_api.py::TestCheckPrimerPair tests/test_agent_api.py::TestDesignPrimersModes tests/test_agent_api.py::TestAgentRegistryIntegrity tests/test_import_layers.py tests/test_audit_2026_09_22b.py::TestAgentEndpointIndexDoesNotDrift` — 91 passed.
- `uv run pytest -q tests/test_public_surface.py` — 3 passed.
- `uv run ruff check .` — passed.
- `PYRIGHT_PYTHON_FORCE_VERSION=latest uv run pyright` — 0 errors.
- `uv run pytest -n auto -q` — 10,411 passed and 10 skipped; 18 tests outside the changed primer paths failed in backup-path, alignment, Babs/UI, bulk-import/export validation, codon UI, heterogeneity, notebook-performance, and cursor-performance coverage.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `456435f80ccc`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.