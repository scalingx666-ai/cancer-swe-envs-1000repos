# Issue

**Title:** Refactor and add PyTorch models

## Description

Will rebase once changes are finalized. Should not merge until after rebase.

Changes:

* Added PyTorch as well as CPU options
* Added tests
* Code style changes
* Uploaded PyTorch models

Comments:

* Currently the code is set up to load and run inference on a single set of 4 images. With a little additional work, we can allow the user to supply multiple sets of images, so it can be immediately useful for (batch) inference. Do we want to do this now?
* We're currently uploading the large model files into GitHub. Do we want to think about putting them on Google Drive or S3 instead?

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `64ec03637d99`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.