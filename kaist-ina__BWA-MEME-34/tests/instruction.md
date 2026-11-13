# Issue

**Title:** feat: ISA-L accelerated FASTQ reader for -8 mode (BWA-MEME2)

## Description

## Summary

Adds a new `-8` mode (**BWA-MEME2**) that replaces the zlib/kseq input pipeline with Intel ISA-L accelerated decompression, memchr-based FASTQ parsing, and arena allocation. This eliminates the I/O bottleneck that emerges at high thread counts (24+ threads), where FASTQ.gz decompression becomes the limiting factor.

> **Terminology**: BWA-MEME = `-7` flag (existing learned index seeding), BWA-MEME2 = `-8` flag (ISA-L fast reader + arena allocator + learned index), BWA-MEM2 = no flag (original).

### Three optimizations
1. **Decompression**: zlib → Intel ISA-L inflate (~85–88% of speedup)
2. **Parsing**: memchr-based vectorized FASTQ delimiter scan (~9–10%)
3. **Allocation**: arena/bump allocator replacing per-read malloc (~2–3%)

### Bug fix: paired-end support (found during @quito418's review)

While testing on bacteria genomes as requested, discovered that the ISA-L fast reader **only opened the R1 file and completely ignored R2** in paired-end mode. This caused `"paired reads have different names"` errors and zero alignments for any paired-end input.

**Root cause**: `fastmap.cpp` opened `fast_reader` for R1 but never created a second reader for R2. The original kseq path uses `ks`/`ks2`, but the `-8` path had no equivalent.

**Fix** (`dda3649`):
- Extracted `fast_reader_next()` single-record parser from the monolithic chunk reader
- Added `fast_reader_read_chunk_pe()` that opens both R1 and R2 with separate ISA-L readers and interleaves records, matching `bseq_read_orig()`'s ks/ks2 behavior
- Added `trim_readno_fast()` for `/1` `/2` suffix trimming (equivalent to kseq's `trim_readno()`)

### Commits
| Commit | Description |
|--------|-------------|
| `b5882fd` | Initial `-8` mode: ISA-L fast reader, arena allocator |
| `7f5efc9` | Remove batch seeding changes, keep only read I/O optimizations |
| `dda3649` | Fix: support paired-end reads in ISA-L fast reader |

## Changes
| File | Change |
|------|--------|
| `Makefile` | Link ISA-L (`-lisal`) |
| `src/fast_reader.cpp` | ISA-L inflate, memchr FASTQ parser, `fast_reader_next()`, `fast_reader_read_chunk_pe()`, `trim_readno_fast()` |
| `src/fast_reader.h` | Public API for fast reader (SE + PE) |
| `src/bwa.cpp` / `src/bwa.h` | Arena allocator (`str_arena_t`) |
| `src/fastmap.cpp` / `src/fastmap.h` | `-8` flag handling, fast_reader open/close for R1 and R2 |
| `src/profiling.cpp` / `src/macro.h` | Read I/O profiling counters |

## Correctness verification

### Bacteria boundary reads (4 genomes, paired-end)

Per @quito418's request — tested on 4 bacteria reference genomes with synthetic paired-end reads at contig boundaries (start offset 0/1/5/10 and end of each contig):

| Species | Contigs | Read pairs | BWA-MEME vs BWA-MEME2 |
|---------|---------|------------|------------------------|
| *A. baumannii* MDR-ZJ06 (GCA_000226275) | 1 | 18 | **PASS** — identical |
| *A. hydrophila* 4AK4 (GCA_000512185) | 1 | 18 | **PASS** — identical |
| *A. macleodii* AD45 (GCA_000300175) | 2 | 36 | **PASS** — identical |
| *B. cereus* G9842 (GCA_000021305) | 3 | 54 | **PASS** — identical |

Full SAM diff (all fields including NM, MD, MC, AS, XS tags): **zero differences**.

### Human genome full-dataset (ERR194147, paired-end, 1.58B alignments)

Reference: human_g1k_v37 (GRCh37). Dataset: ERR194147 paired-end (~97GB compressed FASTQ). Threads: 32.

| Comparison | Lines differ | Result |
|------------|-------------|--------|
| BWA-MEME vs BWA-MEME2 | 0 (core fields) | **PASS** |
| BWA-MEME vs BWA-MEM2 | 172,708 / 1.58B (0.011%) | Expected — different seeding algorithm |

Byte-level comparison (`cmp`) confirmed differences exist only in the `XA:Z` supplementary alignment tag ordering (multithreaded non-determinism). All core alignment fields are identical across all 1.58 billion records.

## Performance benchmark (single-end, ERR194147_1)

Reference: human_g1k_v37. Dataset: ERR194147_1.fastq.gz (~48GB, single-end). Platform: Intel Xeon Silver 4514Y.

| Threads | BWA-MEME2 `-8` (s) | BWA-MEME `-7` (s) | BWA-MEM2 (s) | Speedup vs MEME | Speedup vs MEM2 |
|---------|--------------------:|-------------------:|-------------:|----------------:|----------------:|
| 8  | 3993 | 4308 | 5490 | 1.07x | 1.37x |
| 16 | 2604 | 2707 | 3481 | 1.03x | 1.33x |
| 24 | 2260 | 2478 | 2765 | 1.09x | 1.22x |
| 32 | 1629 | 2337 | 2379 | 1.43x | 1.46x |
| 40 | 1553 | 2364 | 2294 | 1.52x | 1.47x |
| 48 | 1438 | 2404 | 2407 | 1.67x | 1.67x |
| 56 | 1356 | 2387 | 2508 | 1.76x | 1.84x |
| 64 | 1368 | 2457 | 2597 | 1.79x | 1.89x |

**Key observations**:
- BWA-MEME2 scales from 8T to 56T (**2.94x scaling**), remaining compute-bound throughout.
- BWA-MEME and BWA-MEM2 plateau at 32T (~2300-2500s), becoming I/O-bound due to zlib decompression bottleneck.
- At 64T, BWA-MEME2 is **1.79x faster than BWA-MEME** and **1.89x faster than BWA-MEM2**.
- At 8T, BWA-MEME2 is only 7% faster than BWA-MEME (negative control: with few threads, I/O is not the bottleneck, so the ISA-L optimization has minimal impact).
- Minor regression at 64T vs 56T (1368s vs 1356s) likely due to NUMA effects on this dual-socket platform.

## Test plan
- [x] Bacteria boundary test (4 genomes, BWA-MEME vs BWA-MEME2 SAM diff) — per @quito418
- [x] Human genome full-dataset correctness (ERR194147 paired-end, 1.58B alignments)
- [x] Human genome thread-scaling benchmark (8-64 threads, BWA-MEME2 vs BWA-MEME vs BWA-MEM2)
- [ ] Single-end mode regression

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `847a429fcfe3`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.