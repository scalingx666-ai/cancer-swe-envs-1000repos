# Issue

**Title:** Fix blank Venn diagrams for 4–6 set comparisons

## Description

`get_layout()` only defined layouts for 2–3 sets, returning empty `shapes`/`names` for 4–6 sets. Since `DynamicVenn` requests layouts for all sizes up to `max_sets=6`, any report with 4+ comparisons rendered a blank SVG.

## Changes

- **`sequana/viz/venn.py` — `get_layout()`**: Added ellipse-based layouts for 4, 5, and 6 sets:
  - **4 sets**: four rotated ellipses (±30°) in a symmetric 2×2 arrangement with corner name labels
  - **5 sets**: five ellipses at 72° intervals around the centre (computed via `math`)
  - **6 sets**: six ellipses at 60° intervals around the centre (computed via `math`)
  - Updated docstring to reflect supported range (2–6 sets)

- **`test/viz/test_venn.py`**: Added parametrized `test_get_layout[2–6]` asserting each layout returns exactly `n` shapes and `n` name positions with valid ellipse parameters.

- **`test/test_venn_js.py`**: Strengthened `test_dynamic_venn_max_sets` to also assert all six embedded JSON layouts have non-empty `shapes` and `names` arrays.

```python
from sequana.viz.venn import get_layout

for n in range(2, 7):
    layout = get_layout(n)
    assert len(layout["shapes"]) == n   # was 0 for n >= 4
    assert len(layout["names"]) == n    # was 0 for n >= 4
```

<!-- START COPILOT CODING AGENT SUFFIX -->

-

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `225321fc9bd7`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.