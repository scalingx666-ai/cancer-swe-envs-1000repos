# Issue

**Title:** Add Cloudflare Pages previews for pull requests

## Description

Adds a preview link for every pull request into `site`, so reviewers can click through changes before they reach matchminer.org.

- New workflow `.github/workflows/preview.yml`: on each pull request it renders the site with the same pinned Quarto version as the live deploy, uploads it to the Cloudflare Pages project `matchminer-preview`, and comments the preview link on the PR (updated on each push).
- Previews are public but sent with `X-Robots-Tag: noindex`, so search engines skip them.
- Pull requests from forks are skipped, since they don't get repo secrets.
- The live site is unchanged: it still deploys only from `publish.yml` on pushes to `site`.
- CLAUDE.md gets a one-line note about the previews.

This PR should preview itself once the workflow runs.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9348abff57a1`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.