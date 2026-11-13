# Issue

**Title:** Fix Celery workers on macOS with billiard 4.3+

## Description

billiard 4.3 starts pool processes with 'spawn' instead of 'fork' on macOS, breaking the GUI's Celery workers:

- Each pool child gets a pickled copy of the Celery app, including task_cls. But because FlaskTask couldn't be pickled since it was inside the function, causing an exception. Moving it to module level fixes pickling, but also requires looking up the Flask app when a task runs.

- Under 'spawn', Celery only sets up its task tracer in pool children when FORKED_BY_MULTIPROCESSING is set. Without it every task failed with "not enough values to unpack (expected 3, got 0)". Set it in workers._start().

- `oc gui` starts workers with multiprocessing.Process, so in the worker __main__ is '__mp_main__' with no __spec__. billiard then tells its pool children to re-import a module named '__mp_main__', which fails. CPython's multiprocessing handles this case; billiard doesn't. Point __main__ at cravat.gui.workers in that case.

Document FORKED_BY_MULTIPROCESSING in the GUI README for workers started with `celery -A cravat.gui.celery worker`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `854336ae7c87`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.