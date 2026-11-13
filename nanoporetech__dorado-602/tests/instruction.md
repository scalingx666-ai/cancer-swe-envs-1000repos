# Issue

**Title:** Add ModelInfo structure for kit 10.4.1 4kHz 260bps data

## Description

As far as I can tell the stereo model for 260 bps data @ 4kHz is the same as the model for 400 bps model. Unfortunately there is no way to explicitly specify duplex models and increased error checking means you cannot currently stereo basecall your 260 bps data. Therefore I suggest adding a ModelInfo so that this is again possible? If I've got this wrong please do point me in the right direction.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a7fb3e3d4afa`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.