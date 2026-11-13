# Issue

**Title:** fix(jbrowse-web): a plugin install orphaned its web worker pool

## Description

`RpcManager.destroy()` terminates every driver's worker threads, and its docstring names this exact caller:

> Call when discarding the owning root model (e.g. switching sessions or reloading after a plugin change) so orphaned workers don't accumulate.

Nothing called it.

`destroy(rootModel)` did not reach it either, which is why this hid for so long: `rpcManager` is a plain object held as a volatile, and MST teardown only runs what it owns. So the one line that looks like it tears the root down completely does not touch the workers — and **every plugin install left a pool of up to five web workers running for the life of the tab.**

Split out of #5618, where it was found. It is independent of that PR and based on `main`.

### On the test

The test spies on the call rather than watching a thread die, and that is the honest scope of it:

- jsdom has no web workers at all.
- The browser suite cannot see jbrowse's either — `page.workers()`, `browser.targets()` and a `window.Worker` wrapper via `evaluateOnNewDocument` all report **none** of them, with a BAM track open and painting. Filed in `agent-docs/TODO.md`.

But the bug was never that termination was broken; it was that nothing invoked it. The wiring is the whole regression, and the spy pins it — it fails with 0 calls against `main`.

### Checks

- `products/jbrowse-web`: 144 suites / 953 tests pass
- `tsc --noEmit`, eslint, oxfmt clean

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01EjnonUyohzfUV544raMUNo

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fd4bca5c9dee`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.