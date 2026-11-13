# Issue

**Title:** Issue 4570: name archive entries relative to what the selection has in common

## Description

Related to #4570

An archive built for a `DOWNLOAD_ARCHIVE` task no longer carries the folders above what the user selected: picking `R/x86_64-pc-linux-gnu-library/ggplot2/` now unpacks as `ggplot2/...`. What is stripped is the folder the whole selection has in common above the items it names, so two folders of the same name picked in different places keep enough of the tree to tell them apart (`sub1/sub2/folder` with `sub1/sub3/folder` give `sub2/folder/...` and `sub3/folder/...`) and no two different storage paths can collapse onto one entry name. Paths are normalised before anything is taken off them, because stripping a prefix off a path holding `..` is what could otherwise leave an entry name that unpacks outside the folder the user chose.

Test plan
- [x] `~/.venvs/sats/bin/python -m pytest` in `storage-async-task-service` - 250 passed, 1 failed: `tests/test_orchestrator.py::test_never_runs_more_workers_than_there_are_slots`, which fails identically on a clean `java21_migration` tree (verified by stashing, three runs) and is untouched by this change
- [x] `~/.venvs/sats/bin/python -m flake8 sats tests` - clean
- [x] Reviewed by an agent that did not write the change, three passes; its findings on path escaping, the per-file warning and the degenerate entry names are fixed in the diff

Not in this pull request
- UI test cases. The Download-archive feature has none today and the archive's layout is what a user sees after unpacking, so they are owed - skipped on the author's instruction rather than because nothing reaches the GUI.
- Two pre-existing limitations, both reachable only through the REST API and both left alone: a selection naming a folder *and* something inside it lists that file twice, since the sources deliberately do not filter duplicates; and two S3 keys that both climb above the storage root with `..` can still meet under one entry name.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `82371f67fd6f`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.