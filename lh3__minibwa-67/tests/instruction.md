# Issue

**Title:** exit code was always 0 even on error

## Description

`main()` collects each subcommand's return value into `ret` and already uses it — the verbose stats block a few lines above is guarded by `ret == 0` — but then returns 0 unconditionally, so every failure exits successfully.

```
                            before   after
minibwa map --bogus-opt        0       1
minibwa map -x bogus-preset    0       1
minibwa map (normal)           0       0
```

This matters for scripts and pipelines: a mistyped option prints `[ERROR] unknown option in "..."`, maps nothing, and still looks like success to `set -e` or a workflow engine.

Only the propagation is fixed here. Detection is unchanged, and two nearby gaps are left alone: `mem` doesn't diagnose unknown long options at all (it passes no long-option table to `ketopt`), and a missing index still aborts with SIGABRT rather than exiting.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c42d875abd2f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.