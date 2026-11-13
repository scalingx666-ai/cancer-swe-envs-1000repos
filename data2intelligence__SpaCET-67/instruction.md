# Issue

**Title:** Fix fork deadlock with OpenMP-threaded BLAS in parallel steps

## Description

.

## Problem

`SpaCET.deconvolution.matched.scRNAseq` hangs in `generateRef` on the third level-1 lineage, with the progress bar stuck at 0%, on systems where R uses an OpenMP-threaded BLAS (the reporter has FlexiBLAS with the OPENBLAS-OPENMP backend on Rocky 9). `coreNo = 1` does not help.

## Root cause

`pbmcapply::pbmclapply` forks workers. When the parent process has already executed a multi-threaded BLAS call under an OpenMP runtime, GNU libgomp's worker-thread pool does not survive `fork()`: the child inherits the pool bookkeeping but only one thread, and its first threaded BLAS call waits forever at the team barrier.

In `generateRef` the parent-side call is limma's `contrasts.fit`, which computes `coefficients %*% contrasts`. R dispatches that to `dgemv`, and OpenBLAS threads it once `m * n >= 9216` (15884 genes x 2 columns in the reporter's data). That call runs in the parent only for a level-1 lineage that has sub-lineages. The reporter's "Conventional Dendritic Cells" (8 sub-lineages) sits in position 2 in every ordering they tried, so the next fork, position 3, always deadlocks.

`SpatialDeconv` and `SpaCET.CCI.LRNetworkScore` use the same fork pattern. `SpatialDeconv` workers compute `Reference %*% prop`, which becomes a threaded `dgemv` once signature genes x lineages reaches 9216. The bundled Visium reference stays below that, so the built-in pipeline does not hang today; a custom scRNA-seq reference with many lineages and large marker sets would, given any prior threaded BLAS call in the session (for example a Seurat PCA). Pinning is applied at all three fork sites for consistency; it is preventive at the latter two.

## In plain terms

1. **R hands matrix math to a library.** When R computes `A %*% x`, it calls a routine in the BLAS library installed on the machine; on the reporter's system that is OpenBLAS. The matrix-times-vector routine is named `dgemv`.
2. **OpenBLAS decides whether to use helper threads.** For each matrix-times-vector job it counts the numbers in the matrix (rows x columns). Below 9216 it does the job alone on one CPU. At 9216 or more it splits the rows across several CPUs.
3. **limma's matrix has 31768 numbers.** `contrasts.fit` multiplies the coefficient table (one row per gene, two columns: the TT and WT group means) by the contrast vector (1, -1). With 15884 genes that is 15884 x 2 = 31768, above the cutoff, so OpenBLAS splits it.
4. **The helpers are threads that stay alive.** The first time OpenBLAS splits a job it creates helper threads inside the R process. When the job is done they park and wait for the next one. That parked group is the thread pool.
5. **This happens in the parent during a lineage with sub-lineages.** For those, the limma code runs in the main R process, not in a worker. After such a lineage the main process has parked helpers.
6. **Forking copies memory but not threads.** For the next lineage `pbmclapply` forks workers. The fork copies the parent's memory, including the note that says "helpers are parked and ready", but not the helpers. Each worker has one thread and a note about helpers that do not exist.
7. **The worker waits forever.** Inside the worker, limma reaches the same 31768-number multiplication. OpenBLAS sees it is above the cutoff, hands pieces of the job to the helpers, does its own piece, and waits for them to report back. They never do. The worker sits asleep with one thread and no CPU use, which is what `ps` shows on a hung run.

Setting the thread count to 1 in the parent before forking tells OpenBLAS never to split and never to use helpers. The workers inherit that setting, do the multiplication alone, and finish. Nothing gets slower, because 31768 multiply-adds take microseconds either way. Environment variables cannot do this after R has started, because OpenBLAS and the OpenMP runtime read them only once at load.

## Fix

Add `pinBLASThreads()` (R/utilities.R), which sets OpenMP and BLAS threads to 1 via RhpcBLASctl and returns a restore closure, and call it at the top of the three functions that fork (`generateRef`, `SpatialDeconv`, `SpaCET.CCI.LRNetworkScore`) with `on.exit()` restore. RhpcBLASctl is added to Imports.

Why RhpcBLASctl: `Sys.setenv(OMP_NUM_THREADS = 1)` has no effect once R has started, because libgomp and OpenBLAS read the variable only at library load. `omp_set_num_threads(1)` at runtime does work, because OpenBLAS's OpenMP build follows `omp_get_max_threads()` and libgomp skips the pool entirely for single-thread regions.

Performance: process-level parallelism across `coreNo` workers is unchanged. The BLAS calls on these paths are too small to benefit from threading (`lmFit` uses LINPACK `dqrls` with vector length = number of cells, which OpenBLAS does not thread below 10000), and pinning also stops each forked worker from starting its own full-size OpenMP pool. Per-lineage timings on the reporter's data are identical before and after.

## Verification

Reporter's data (from the issue's Dropbox link), unmodified `generateRef` from `main`, R 4.3 with an OpenBLAS 0.3.21 `USE_OPENMP=1` build preloaded, `OMP_NUM_THREADS=4`, `coreNo = 4`:

| run | result |
|---|---|
| `main` | B Cells 9 s, Conventional Dendritic Cells 23 s, then stuck at Endothelial Cells (killed after 300 s; 4 workers each with 1 thread, sleeping) |
| `main` + `RhpcBLASctl::omp_set_num_threads(1)` before the call | all 10 lineages, 2 min 21 s |
| this branch | all 10 lineages, 2 min 33 s |

Direct test of the mechanism (C, `cblas_dgemv` 15884 x 2, fork, `dgemv` in the child):

| parent before fork | child |
|---|---|
| no BLAS call | finishes |
| dgemv below threshold (m*n = 8000) | finishes |
| dgemv above threshold (m*n = 31768) | hangs |
| above threshold, then `setenv OMP_NUM_THREADS=1` | hangs |
| above threshold, then `omp_set_num_threads(1)` | finishes |

`SpaCET.deconvolution` on the bundled Visium_BC example, same BLAS setup, with a threaded `dgemv` executed in the parent first:

| run | result |
|---|---|
| `main` | completes: 35 cell types x 3813 spots, 4 min 54 s. No deadlock here because the built-in reference's level-1 signature x lineages is below the `dgemv` threading threshold, so the workers never enter a parallel region |
| this branch | completes: 35 cell types x 3813 spots, 4 min 37 s end to end |

## Workaround for users on affected systems (without this patch)

Export `OMP_NUM_THREADS=1` before starting R or RStudio Server, or call `RhpcBLASctl::omp_set_num_threads(1)` at the top of the script. Setting the variable from inside R does nothing.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0199d93c23c6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.