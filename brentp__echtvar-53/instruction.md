# Issue

**Title:** ARM support: use Scalar stream-vbyte on non-x86, SIMD on x86_64

## Description

- Remove x86-only stream-vbyte features from default deps for macOS ARM
- Gate x86 SIMD (Ssse3 decode, Sse41 encode) on target_arch = x86_64
- Fix Cargo.toml: move target-specific deps to end so other deps apply on all targets

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f37761117571`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.