# Issue

**Title:** Add compatibility for Histogan

## Description

This version differs slightly from the original PR in that it does not require manual editing of feature extractors you want to be compatible. An example of how to enable histogan compatibility:

```python
uni = sf.build_feature_extractor('uni', ...)
uni.force_uint8 = False
uni.inference_mode = False
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5bfd19c9274d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.