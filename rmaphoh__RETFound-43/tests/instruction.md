# Issue

**Title:** Fixes for latent_feature.ipynb

## Description

Hi!
Thank you for your amazing work with RETFound! The latent_feature notebook is very organized and easy to use. This pull request fixes some bugs I encountered and wanted to share to make it easier for other users of RETFound.

- The `arch` argument was set to a previous version's `vit_large_patch16`. Changing this to `RETFound_mae` correctly references the model architecture in `models_vit.py`.
- PyTorch >= 2.6 changed the default value of `weights_only` in `torch.load()` to True. Passing False to `torch.load()` allows for use with newer PyTorch version.
- For the convenience of non-GPU users select CPU as the device if CUDA is not available.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `91915d6a1410`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.