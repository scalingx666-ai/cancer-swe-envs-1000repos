# Issue

**Title:** Add the missing `watch` script and drop stale README build advice

## Description

## Problem

`README.md` and `docs/site/faq.md` both tell developers to run `yarn watch` / `npm run watch` while editing source. The FAQ even explains what it does:

> In modify JBrowse source code you must use `npm run watch` (equivalently `yarn watch`) to watch for changes to the codebase. This uses `webpack -w` in the background...

**But there is no `watch` script in `package.json`**, so both commands just error out. Anyone following the developer instructions hits a dead end.

The README's build note was also stale in both directions:

- It warns to use *node <=14* because of node-sass — but node-sass was removed in 1.17.0.
- It says you "may need to run `export NODE_OPTIONS=--openssl-legacy-provider`" — but `build/run-webpack.js` has been injecting that automatically for node >=17 since then.

## Changes

- Add `"watch": "node build/run-webpack.js webpack --watch"`, mirroring `build` so it routes through `run-webpack.js` and inherits the automatic `--openssl-legacy-provider` handling. This makes the already-documented workflow real rather than deleting it from the docs.
- Replace the stale README note with what is actually true today.

## Testing

- `npm run watch` builds `dist/` with 0 errors and stays running to watch, as the FAQ describes.
- The webpack build itself verified on **node 12.22** and **node 24** (the README's "node 12 through node 24" claim is grounded at both ends).
- `prettier --check` clean on `package.json` and `README.md`. `release-notes.md` was already prettier-unclean at HEAD, so it is deliberately not reformatted here.

No install-path changes: `setup.sh`, the lockfile, and CI are untouched.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01VGHDpMp2TPeDdriLJoYNYf

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3193a9607a61`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.