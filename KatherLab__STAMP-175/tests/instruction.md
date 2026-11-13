# Issue

**Title:** Dev/prebuilt flash att

## Description

Set up installation with pre-built wheels for flash_attn 2.8.3 for x86_64 and aarch64. Installation now takes less than 10min then we can consider putting it in `--extra gpu`

Wheels are taken from: https://github.com/mjun0812/flash-attention-prebuild-wheels

Tests have been successful on Planets but failed with Github. I hard-code `--extra cpu` in build.yml

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c54ce0673962`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.