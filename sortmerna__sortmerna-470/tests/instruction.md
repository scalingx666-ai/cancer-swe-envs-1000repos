# Issue

**Title:** Pin librapidarchive, BBHash, cxxopts and parasail

## Description

`3rdparty.jinja` clones librapidarchive, BBHash, cxxopts and parasail at `master`, so what a build gets depends on the day it runs. Two have already moved since v8.0.1 was tagged: cxxopts is at `ad6e413` and librapidarchive at `d1709bc`.

This pins each at the commit that was `master` when v8.0.1 was tagged:

| Dependency | Commit |
|---|---|
| librapidarchive | `9965b1d` (includes the issue-466 fix, 2e2761b) |
| BBHash | `be4220c` |
| cxxopts | `bb79154` |
| parasail | `fb985ee` |

- `git_clone` takes an optional `commit` and checks it out, after a fresh clone or on an existing one. The four dependency steps pass the `commit` from `3rdparty.jinja`; zlib and RocksDB are unchanged.
- cxxopts cannot be the v3.3.1 tag: `normalize_argv` writes options such as `-N=-3`, which cxxopts parses only since jarro2783/cxxopts#488. With v3.3.1 they fail with "Option '=' does not exist".

### Tests

On macOS arm64:
- `python setup.py indexed_bzip2|bbhash|cxxopts|parasail` from a fresh checkout leaves each at its pin, with librapidarchive's own submodules at that commit's versions, and builds parasail.
- Rerunning on clones moved to `master` moves them back to the pins.
- An unknown commit returns non-zero, which stops `setup.py all`.
- `setup.py all` was not run end to end. These four commits are the ones our downstream build of 8.0.1 uses.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `34efbb853a2b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.