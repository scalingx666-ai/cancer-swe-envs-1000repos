# Issue

**Title:** chore: prepare 0.37.0 release

## Description

## Description

Prepare polars-bio 0.37.0 by synchronizing the Python and Rust package versions and both lockfiles, and moving the unreleased changelog into a dated release entry. The notes cover Polars 2.0/2.1 support, owned frame metadata, coordinate-safe tabular readers, and the fixes and dependency updates merged since 0.36.2.

Refresh the developer dependency pins and document the Bioconda handoff. Add the two missing parameter types in the CSV reader docstring so the strict documentation build passes.

## Type of change

- [x] Documentation update
- [x] Refactor / chore / CI (no functional change)

## How has this been tested?

Validated from a clean copy of tracked source on macOS arm64, using Python 3.12.2 and Polars 2.1.0:

- `make test-no-sync`: main suite **2,601 passed, 6 skipped**; isolated overlap, warnings, and streaming suites **15 / 11 / 37 passed**.
- `maturin build --release --locked` and `maturin sdist`: both artifacts build with version 0.37.0, the owned metadata provider and its license, and no `polars-config-meta` runtime requirement.
- Fresh wheel installation without `polars-config-meta`: CSV/group/range/Parquet workflows, nested schema metadata, VCF round trip, and the Bioconda recipe's Python smoke commands pass. `uv pip check` passes.
- `mkdocs build --strict`: passes with the local Cairo library path configured.
- `uv lock --check --offline`, locked Cargo metadata validation, version/recipe consistency checks, Ruff lint/format checks, `git diff --check`, and commit hooks pass.

## Additional notes

The upstream Bioconda recipe needs a manual update alongside the published 0.37.0 sdist: remove `polars-config-meta`, require `polars>=1.40.0,<2.2`, and include the bundled metadata-provider license. These requirements are already present in the local staged recipe. Update the source version and SHA256 together once the artifact is published; autobump does not update dependencies. No build-script change or removal of the standalone conda-forge package is needed.

This PR prepares the release; it does not create a release tag or publish packages.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `875d990a9f45`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.