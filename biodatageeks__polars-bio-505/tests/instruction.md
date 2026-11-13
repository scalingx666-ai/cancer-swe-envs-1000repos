# Issue

**Title:** fix: stop caching the config_meta accessor on frames

## Description

.

## Problem
Polars' `NameSpace.__get__` caches the accessor on the instance (`setattr(instance, "config_meta", accessor)`), and `FrameMetadata` holds a strong `_owner` reference to its frame. That frame → accessor → frame cycle means a frame whose `config_meta` was touched (even a read-only `get_metadata()`) is not freed by reference counting. It waits for the cyclic GC, which is triggered by allocation counts rather than memory, so loops over large tagged frames accumulate native memory.

polars-bio's own code paths (`io.py`, `_metadata.py`) already use the `__dict__` helpers and were unaffected. The leak hit user code that calls `df.config_meta`, which is the API our error hints and docstrings tell users to call.

## Fix
`initialize()` still registers the namespace through `pl.api.register_*_namespace`, keeping Polars' validation, the `_accessors` bookkeeping and the failure-injection points used by the rollback tests. It then replaces the descriptor with `_MetadataNamespace`, which returns a fresh `FrameMetadata(instance)` on every access and never stores it on the frame. The descriptor keeps `_ns`, so `_check_namespace_ownership()` and the rollback check work unchanged.

The strong owner stays, so `pl.DataFrame(...).config_meta.get_metadata()` on a temporary frame still works.

**Behaviour change:** `df.config_meta is df.config_meta` is now `False`. `FrameMetadata` keeps no state of its own (it re-reads the frame's dict on each call), so this has no other effect, and nothing in the repo relies on identity.

## Verification
Issue reproducer (10 × ~160 MB frames, Polars 1.44.2, Python 3.12, macOS arm64):

| | freed on `del` | peak RSS |
|---|---|---|
| no metadata | yes | 328 MB |
| `config_meta.set(...)`, master | no | 1701 MB |
| `config_meta.get_metadata()`, master | no | 1701 MB |
| `config_meta.set(...)`, this PR | yes | 327 MB |

- New regression test `test_accessor_is_not_cached_and_frame_is_freed_by_refcount` (DataFrame + LazyFrame) asserts that the accessor is not in `frame.__dict__` and that the frame is freed with `gc.disable()`. It fails on master and passes here.
- `tests/test_frame_metadata.py` passes on Polars 1.40.1, 1.44.2 and 2.1.0.
- Full suite (excluding `test_streaming.py`): 2567 passed, 1 skipped. The 5 `test_overlap_algorithms.py::*_log` failures also occur on unmodified master (order-dependent; they pass in isolation) and are unrelated.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `6f75152a9e2b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.