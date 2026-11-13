# Issue

**Title:** Record GPN 0.9.0 publication

## Description

## Outcome

Record the completed GPN 0.9.0 publication after the exact reviewed release candidate was tagged and published through Trusted Publishing.

## Publication evidence

- Release: https://github.com/songlab-cal/gpn/releases/tag/v0.9.0
- PyPI: https://pypi.org/project/gpn/0.9.0/
- Workflow: https://github.com/songlab-cal/gpn/actions/runs/32965467513
- Release commit: `007768a31618fa76c2c3db953e69cc2013f5a79c`
- Release tree: `8595b87d599c3e7fcbfc599352b5c6ab9e2f8350`
- Annotated tag object: `37ac68ce7b1d8b7365380401aa89993017864024`
- Wheel SHA-256: `7a175368577a851593bacca774caa80da3185aea375a0ab25fcf12147ecddd47`
- Source distribution SHA-256: `ad3c4ed9cc1013b26675b55f9f81b14329b5c4ef2344db1dd5d7725b52442316`

The PyPI files match the immutable workflow artifact byte-for-byte. Both distributions pass PyPI attestation verification against `songlab-cal/gpn`. A clean Python 3.13 CPU install from PyPI reports `0.9.0`; CLI help/version and explicit AutoClass registration pass. Read the Docs returns HTTP 200.

## Validation

- `uv run pre-commit run --all-files`
- `uv run pytest` — 234 passed, 6 skipped
- `python docs/prepare_notebooks.py`
- `uv run sphinx-build -n -W --keep-going -b html docs docs/_build/html`

This PR contains records and their governance assertions only; it does not alter the already-published artifacts. Issues #81 and #108 remain open for post-release work.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `007768a31618`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.