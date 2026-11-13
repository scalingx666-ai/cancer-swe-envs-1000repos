# Issue

**Title:** ENH: Print data ID and full precision on mesh test data mismatch

## Description

Print the point/cell ID and full-precision values when mesh IO tests find mismatched point or cell data, so intermittent failures like `itkMeshFileReadWriteTestGifti2` on macOS can be diagnosed.

<details>
<summary>Motivation</summary>

`itkMeshFileReadWriteTestGifti2` fails intermittently on macOS (arm64 nightly on 2026-08-09 and 2026-09-14, and an x86_64 Rosetta CI job on 2026-11-12). The `itk::Mesh` pass succeeds and the `itk::QuadEdgeMesh` pass fails on byte-identical files, reporting `Input = 1.31602e+06` and `Output = 1.31602e+06`. Default 6-digit output hides the actual difference and the failing index. The written file contains only the correct label key (1316020) in that range, so the corruption happens at read time. The root cause is not identified yet.

</details>

<details>
<summary>AI assistance</summary>

- Tool: Claude Code
- Role: analyzed the CI failure, ruled out endianness, int-to-float precision and pipeline re-execution, and wrote this diagnostic change
- Testing: compiled `itkMeshFileReadWriteTest.cxx` against the edited header with MSVC (`/Zs`); ran the existing test 8 times locally on Windows (all passed); pre-commit hooks pass

</details>

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b621f7c0068f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.