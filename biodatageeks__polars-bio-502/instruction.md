# Issue

**Title:** chore(conda): sync bioconda recipe with upstream 0.37.0

## Description

Syncs `bioconda-recipe/` with the upstream recipe as updated in bioconda/bioconda-recipes#71352.

**`meta.yaml`** now matches upstream:
- version 0.37.0 with its PyPI sdist sha256; the placeholder 0.33.1 source and the "staged for 0.37.0" note are gone
- run deps: `polars >=1.40.0,<2.2`, no `polars-config-meta`
- `polars_bio/licenses/polars-config-meta/LICENSE` in `license_file`
- `additional-platforms`: `osx-arm64` only. The local copy also listed `linux-aarch64`, which the live recipe has never built.

The one difference from upstream is a comment. Upstream says linux-aarch64 is left out "because nothing upstream exercises ARM Linux yet". That is outdated: `publish_to_pypi.yml` runs `linux_arm64_tests` on `ubuntu-24.04-arm`. The comment here gives the actual reason instead: bioconda has never built that platform, and a failure there would block release bumps. The corrected comment can go upstream with the next real recipe change. A comment-only push to #71352 would have restarted its builds.

Rendered with conda-forge pinning, the recipe matches #71352's line for line, apart from the order conda-render prints them in.

**`README.md`**:
- drops `test_overlap.py` from the contents table; it no longer exists and the smoke test is inlined
- Platforms section now says the recipe opts in to `osx-arm64` only
- replaces the 0.37.0 handoff checklist, now done, with the procedure for releases that change run deps: a replacement PR from a fork plus a superseding comment on the autobump PR, and a quick wheel-based check of the dependency bounds and test commands

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `d142e6bc2c50`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.