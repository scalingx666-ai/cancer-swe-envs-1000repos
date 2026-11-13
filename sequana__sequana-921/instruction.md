# Issue

**Title:** Fix reversed translation in `Chain.align_to()` superposition output

## Description

`Chain.align_to()` computed the translation vector in the opposite direction of the rotation returned by `superpose(coords2, coords1)`. As a result, alignments looked correct at RMSD level but produced incorrect geometry when reapplied through `Alignment.apply_to_structure()`.

- **Alignment math**
  - Correct the translation term in `sequana/pdb.py` so the returned rigid transform maps the mobile chain onto the target chain consistently with the rotation matrix.

- **Regression coverage**
  - Add focused coverage for the previously untested path:
    - build two small in-memory chains with known rotation/translation relationship
    - verify `Chain.align_to()` returns aligned coordinates in target space
    - verify `Alignment.apply_to_structure()` reproduces the target structure coordinates

- **Behavioral impact**
  - Makes the transform returned by `Chain.align_to()` safe to reuse for full-structure superposition, which was the broken case behind this issue.

```python
rotated, R, rmsd_val = superpose(coords2, coords1)

# translation must map coords1 onto coords2 after rotation
translation = np.mean(coords2 - (coords1 @ R.T), axis=0)
```

<!-- START COPILOT CODING AGENT SUFFIX -->

-

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `225321fc9bd7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.