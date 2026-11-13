# Issue

**Title:** Fix: Load model checkpoint dynamically on the correct device

## Description

This PR fixes a device mismatch issue when loading model checkpoints. The update ensures checkpoints are mapped to the same device as the network, preventing errors when switching between CPU and GPU.

## Changes:
- Dynamically map checkpoint to `network.parameters().device`.
## Why:
- Fixes crashes when loading GPU-trained models on CPU.
- Ensures seamless CPU/GPU compatibility.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `818e29b860c4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.