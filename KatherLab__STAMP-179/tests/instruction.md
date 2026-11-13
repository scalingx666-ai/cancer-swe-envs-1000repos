# Issue

**Title:** Modernise the dependency stack and pin it exactly

## Description

- Python 3.13/3.14, PyTorch 2.11, current runtime dependencies
- `flash-attn` / `mamba-ssm` / `causal-conv1d` from pre-built wheels at `https://wheels.astral.sh/simple/cu130/` instead of source builds
- `transformers` held at 4.57 (transformers 5 requires `all_tied_weights_keys`, absent in the TITAN/PRISM remote-code models), `huggingface-hub<1.0` to match
- Every requirement pinned to `==`, enforced by `scripts/check_dependency_config.py`
- CI: static dependency checks, CPU matrix, GPU extras without a driver, aarch64

Verified on aarch64/GB10 and x86_64/RTX A6000: `uv sync --locked --extra gpu_all` is wheels-only, torch 2.11.0+cu130 runs on GPU, full suite green including 21/21 extractor tests.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a410d2762915`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.