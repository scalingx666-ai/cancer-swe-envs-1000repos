# Issue

**Title:** [fix] Fix multiple API endpoint issues

## Description

- Fix web_search endpoints asyncio event loop error (use run_async instead of run)
- Fix visualize_molecule/protein/pocket path (core/visualize.py -> tools/visualization_tools.py)
- Fix protein_binding_site_prediction:
  - Replace pandas CSV read with manual parsing (numpy compatibility)
  - Add PDB residue number to protein.residues index mapping
- Uncomment healthz endpoint for service health check
- Add API test script with configurable URL parameter
- Add 3D visualization config file

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3094e9b82d4d`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.