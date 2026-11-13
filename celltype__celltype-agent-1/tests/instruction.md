# Issue

**Title:** fix: install from GitHub repo instead of PyPI

## Description

## Summary

- **Fix install script failing** because `celltype-cli` is not published on PyPI — `uv tool install celltype-cli` and `pipx install celltype-cli` both fail with "No solution found when resolving dependencies"
- Install directly from the GitHub repository using `git+https://github.com/celltype/cli.git` URLs
- Prefer `uv` over `pipx` (faster, more widely available)

## What changed

- Added `REPO_URL` variable pointing to `git+https://github.com/celltype/cli.git`
- Updated `uv tool install`, `pipx install`, and `pip install` commands to use the git URL
- Swapped preference order: `uv` → `pipx` → `pip` (was `pipx` → `uv` → `pip`)
- Use `--force` flag for re-installs/upgrades instead of separate upgrade commands

## Test plan

- [ ] Run `curl -fsSL https://raw.githubusercontent.com/naofel1/cli/fix/install-from-github/install.sh | bash` on macOS with uv installed
- [ ] Run on a machine with only pipx
- [ ] Run on a machine with only pip
- [ ] Verify `ct --version` works after install

Made with [Cursor](https://cursor.com)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `21b91bc727a6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.