# Issue

**Title:** Add -threads support to unoise3/uchime3_denovo chimera stage

## Description

`usearch -unoise3` (and `-uchime3_denovo`) currently ignores `-threads` — the CLI reports `WARNING: Option(s) set but not used: -threads`. The de novo chimera stage is the dominant cost of unoise3: it is a per-query, serial, full-alignment linear scan over a growing search DB. On a 134,940-amplicon 16S dataset it takes ~6–8 h single-threaded while the rest of the pipeline takes minutes. This patch makes the chimera stage parallel.

## What changed

**1. Add -threads support to unoise3/uchime3_denovo chimera stage**
- `DeParser::ParseLo` is split into a serial scan, a parallel scan, and a post-scan step.
- The parallel scan uses a persistent worker pool (`ChimeraPool`): each worker has its own `ObjMgr`/`GlobalAligner`/`DeParser` and scans a contiguous chunk of the search DB, accumulating results with the same strict-comparison, first-wins tie-breaking as the serial loop (DiffsQT min; left positions max; right positions min).
- Merging chunk results in index order reproduces the serial state exactly (the serial early break at DiffsQT==0 is emulated with an `ExactFound` flag plus truncating merge), so **outputs are byte-identical for any thread count**.
- Thread count comes from `GetRequestedThreadCount()` (i.e. `-threads`, with the same defaults as the other usearch commands). The scan stays serial for search DBs below 256 targets or when `-uchimeout`/`-alnout` debug output is requested.

**2. Fix shared-query data race in parallel chimera scan** (found while validating the first version, which segfaulted at 64 threads)
- The alignment path refcounts and allocates through `Query.m_Owner`: `GlobalAlign_AllOpts` takes its `SubPath` from the query's owner, and `AlignResult::Create/Down` Up/Down the query. Sharing one query `SeqInfo` across all workers raced on the main thread's `ObjMgr` pool and the query's refcount, corrupting alignment paths (assert `QPos == QL && TPos == TL`) or segfaulting.
- Each worker now makes a deep copy of the query in its own `ObjMgr` (`SeqInfo::Copy`), matching the per-thread-query idiom of the other parallel commands (e.g. `derepfull`).

## Verification

Real 16S amplicon data, 20,000-sequence subset, full `unoise3` run (denoise + chimera), compared against the unpatched v12.0-beta1 binary:

| threads | total wall time | chimera stage | output vs unpatched |
|---:|---:|---:|---|
| 1 | 244.7 s | 236 s | byte-identical |
| 16 | 37.5 s | 29 s | byte-identical |
| 64 | 27.7 s | 18 s (13.1×) | byte-identical |

Both `-zotus` and `-tabbedout` outputs are byte-identical at all three thread counts, and the "Option not used" warning is gone. Full dataset (134,940-amplicon production input, same 256-core machine): a serial v11 run on this data reached 59.7% of the chimera stage after 4h20m elapsed (6–8 h projected). With `-threads 64`, the full run finished in 55:08 — denoise (inherently serial) 34:47, chimera stage 20:20 (~18× the serial projection), exit 0, 51,192 final sequences.

I'm using this in a production 16S denoising pipeline; happy to discuss the design (e.g. the 256-target serial-fallback threshold, the worker pool lifetime) if you'd prefer a different shape.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `304cce68f19a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.