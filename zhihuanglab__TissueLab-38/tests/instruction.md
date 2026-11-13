# Issue

**Title:** ST counting workflow: CellCharter wiring, slide mpp to the coding agent

## Description

## Summary

Wiring for the CellCharter spatial-omics node (Model Zoo PR `feat/cellcharter-node`): the registry entry that already existed now says what the node takes and writes, has panel fields for the `.h5ad` path and K, and the code prompt documents the `Spatial-Omics` layout.

- **Registry (preset + fallback)**: CellCharter description, `zarr_group: Spatial-Omics`, inputs (`st_path`, `n_clusters`), outputs (`clusters/k<K>`, `centroids`, `cluster_markers/k<K>`, `nucleus_id`, `segmentation_index`), panel fields `st_path` (empty = the `.h5ad` next to the slide) and `n_clusters` (default 9).
- **Slide mpp to the coding agent**: the viewer's slide mpp reached only the planner (`data_context.slide_info`); the coding step saw it only when a node had written it into the zarr, so scripts guessed a calibration. The chat now puts `slide_mpp` on the CodingAgent step (hidden panel field, like `web_search_enabled`); `start_workflow` and `generate_script`carry it to script generation, which appends "Slide calibration: <mpp> microns per pixel at level 0" to the task text (with a note to say so and derive scales from the data if the value is implausible).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2b316489684d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.