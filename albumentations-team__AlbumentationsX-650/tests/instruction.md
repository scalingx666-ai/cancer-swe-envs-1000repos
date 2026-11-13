# Issue

**Title:** Use the Albucore CPU NumPy–Torch bridge

## Description

Use the CPU NumPy–Torch bridge from [Albucore 0.3.6](https://github.com/albumentations-team/albucore/releases/tag/0.3.6) in `ToTensorV2`, `ToTensor3D`, Tensor fallback, annotations, and medical FFT and noise paths. Terminal transforms request contiguous outputs. Fallback retains compatible strided views. AX owns the target layout and optional channel axes.

Pin 0.3.6 in the Python and Conda manifests and lockfile. The PyPI wheel and sdist match the previously reviewed MIT license evidence. Albucore remains a separately installed dependency.

The existing `check-ax-rules` pre-commit hook enforces the bridge through `AXG028`. It rejects direct `torch.from_numpy` and `.numpy` access in `albumentations/`. The 78 coding-guidance and AX rule tests passed.

### Performance

M4 Max, Python 3.11.15, NumPy 2.4.6, Torch 2.15.0, and OpenCV 5.0.0.93, one thread. Median µs per paired Compose call, old AX conversion → Albucore bridge.

| Input | uint8 | float16 | float32 |
| --- | ---: | ---: | ---: |
| RGB image, 256×256 | 57.4 → 15.0 | 58.1 → 22.4 | 58.7 → 36.4 |
| Four RGB images after vertical flip, 224×240 | 203.8 → 55.7 | 204.3 → 87.3 | 216.7 → 153.6 |
| Four 3D masks, 16×128×128×3 | 822.3 → 120.8 | 842.6 → 237.7 | 897.6 → 472.0 |

Tensor-input crops were 1.16–1.21× faster. Already-dense single-channel controls usually added about 0.3 µs, with one volume control adding 0.94 µs. RicianNoise and MotionArtifact matched byte for byte in 12 paired cases. An initial MotionArtifact float16 Compose run measured 5.4% slower. The isolated repeat measured 16.55 → 16.52 ms.

### Verification

- 307 bitwise Core and Compose comparisons and 40 fallback cases, including stride and storage sharing checks. Added tests for arbitrary float bit patterns, cropped inputs, negative singleton strides, and writable vs read-only mask storage.
- 1,003 focused tests, 6,855 contract and regression tests, and 51 CI tooling tests passed. The final terminal test run passed 50 tests, including the two added storage ownership cases.
- Pre-commit, mypy, Pyrefly, wheel and sdist verification, and an installed-wheel smoke test passed.

## Summary by Sourcery

Standardize CPU NumPy–Torch conversions on Albucore 0.3.6 while preserving target layouts, compatible storage sharing, and tensor output guarantees.

New Features:
- Adopt Albucore 0.3.6 CPU NumPy–Torch bridge conversions across tensor transforms, fallback processing, annotations, and medical processing paths.
- Add AXG028 guidance checks to enforce the shared tensor bridge within Albumentations.

Bug Fixes:
- Preserve tensor data and storage semantics for strided, read-only, negative-stride, and arbitrary floating-point NumPy inputs.

Enhancements:
- Centralize tensor target layout and channel-axis metadata while retaining compatible zero-copy views and requiring contiguous terminal tensor outputs.
- Document the NumPy–Tensor conversion and storage-routing contract.

Build:
- Pin Albucore to version 0.3.6 in Python and Conda dependency manifests and the lockfile.

CI:
- Extend coding-guidance tests to validate tensor bridge enforcement and permitted usage.

Documentation:
- Update contributor and tensor-routing documentation for the Albucore CPU bridge and storage behavior.

Tests:
- Add coverage for bit preservation, cropped and flipped inputs, singleton negative strides, storage sharing, and 3D tensor conversions.

Chores:
- Update dependency license metadata for the Albucore upgrade.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->
<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **Bug Fixes**
  * Improved conversion of images, masks, volumes, and vector fields to tensors, preserving values, data types, and expected layouts for batched and unbatched inputs.
  * Improved handling of read-only arrays and arrays with unusual strides, including after cropping or flipping, while maintaining expected output values and storage behavior.
* **Documentation**
  * Clarified how array-to-tensor conversion handles storage, layouts, and array compatibility.
  * Added guidance for choosing conversion approaches when working with NumPy arrays and tensors.
<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c7c1e506966c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.