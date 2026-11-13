# Issue

**Title:** Installation & Docs Updates

## Description

Various updates required for clean install & to update the ReadTheDocs: 

Changes: 
- Removed stale Large File Storage (LFS) tracking that was in the .gitattributes file (not required because the tests are small) 
- Migrated `setup.py` to `pyproject.toml` (setup.py is deprecated) & updated doc reference (python setup.py install to pip install .) 
- Added `.readthedocs.yaml` -> since Jan 2025 ReadTheDocs requires a config file, so added this. 

Verification: 
- Tested fresh venv install, succeeds & sphinx -b html docs/source build successfully.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `bcc12a57458f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.