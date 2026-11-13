# Issue

**Title:** Update Vapor Dockerfile and WDL

## Description

We optimized Vapor () and reduced its execution cost (~15x faster)

This PR builds on that, updating the Dockerfile and WDL to use the optimized Vapor.

Specifically: 

* Changes in the Dockerfile: 

  - **Base image:** Ubuntu 18.04 → 22.04.
  - **samtools/bcftools:** 1.9 → 1.24, built from source. htslib 1.9 cannot fetch remote
  (`gs://`, `https://`) indexes with 22.04's libcurl.
  - **gcloud:** `google-cloud-sdk=239.0.0` is no longer published, so the image installs
  `google-cloud-cli`. The Python 2 pip steps and `apt-key` are replaced with their 22.04
  equivalents.
  - **vapor:** installed from talkowski-lab/vapor at `VAPOR_COMMIT`, into a Python 3.6 environment
  provided by micromamba. Its libraries are pinned to the versions of the previous image, so scores
  do not change: numpy 1.19.5, scipy 1.5.4, scikit-learn 0.24.2, matplotlib 3.3.4 and Cython
  0.29.37, plus pysam 0.23.0.
  - **Build fixes:** the old recipe no longer built. Its rpy2 dependency (never used by vapor) cannot
  be installed on Python 3.6, and a current Cython miscompiles 5e322b5.
  - **Threads:** `OMP_NUM_THREADS=1` (and the OpenBLAS/MKL equivalents), so each process uses one
  native thread.

* Changes in the WDL:

  - **Plots off by default:** `save_plots` now defaults to `false`.
  - **Plot setting reaches the tool:** `save_plots` is passed to `RunVaporWithCram`, which runs vapor
  with `--no-plots` when it is false. Previously every shard drew, tarred and merged all plots, and
  the workflow discarded them at the end. Each shard still writes an (empty) plot tarball, so task
  outputs and `ConcatVapor` are unchanged.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c0314afad9e0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.