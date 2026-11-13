# Issue

**Title:** Require stride-aware backends for pandas 3.1

## Description

pandas 3.1 can return non-contiguous arrays from Series.values, which older ncls, sorted_nearest and pyrle kernels reject. Require the fixed backend versions so k_nearest, overlap, subtraction and coverage work without adding copies throughout PyRanges.

Bumps PyRanges to 0.1.7 and requires ncls >= 0.0.71, sorted_nearest >= 0.0.42 and pyrle >= 0.0.46 for the coverage extra.

Prerequisites: merge and publish the backend fixes before merging/releasing this dependency update:
- ncls:
- sorted_nearest:
- pyrle:

Validation: smoke-tested k_nearest, overlap, join, subtract, coverage and to_rle on Python 3.12 / pandas 3.1.0 with wheels built from those fixes. The older k_nearest.py tests retain three pre-existing int32-versus-int64 fixture mismatches, reproduced with the previous backend/PyRanges versions; those fixtures are unchanged here.

CI now tests Python 3.11 and above and installs pinned companion backend PR revisions before their releases are available on PyPI. Add a local tests package marker so dependency test packages cannot shadow tests.helpers. Local validation: 87 doctests and 40 unit tests pass.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9999c1a9040b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.