# Issue

**Title:** feat: add fermikit single-thread option

## Description

This is a re-creation of  for merging into the upstream.

This PR has been (largely) created using Copilot, but I have reviewed all changes and have run the example/test_all.sh script on this code.

## Original text from copilot

The genotyping pipeline re-aligns reads against a de-novo HLA assembly, but fermikit assembly can vary across runs when multi-threaded. This change adds an explicit option to keep the overall pipeline threaded while forcing the fermikit assembly step itself to run single-threaded for reproducible contig construction.

- **New CLI control**
  - Adds `-F` to `script/whole/SpecHLA.sh` to force the fermikit de-novo assembly stage to run with one thread.
  - Mirrors the same option in `script/whole/test_SpecHLA.sh` to keep the test entrypoint aligned with the main CLI.

- **Scoped threading change**
  - Passes the new flag through to `script/run.assembly.realign.sh`.
  - Applies the override only to `fermi2.pl unitig`.
  - Leaves all other thread-aware commands in the re-alignment stage on the user-provided `-j` thread count.

- **Documentation**
  - Updates CLI help text and `README.MD` to expose the new option and intended behavior.

Example:

```bash
# Keep the pipeline at 8 threads, but force fermikit assembly to use 1
bash script/whole/SpecHLA.sh -n sample -1 sample.R1.fq.gz -2 sample.R2.fq.gz -j 8 -F
```

<!-- START COPILOT ORIGINAL PROMPT -->



<details>

<summary>Original prompt</summary>

> During genotyping, there is a re-alignment step to a de-novo assembly of the HLA regions. Plase add an option to force the fermikit de-novo assembly step to always run single-threaded regardless of the threads provided to the genotyping command. The intention is to ensure that this always runs reproducibly, as fermikit is known to be non-deterministic in constructing assemblies.


</details>



<!-- START COPILOT CODING AGENT SUFFIX -->

Created from [VS Code](https://code.visualstudio.com/docs/copilot/copilot-coding-agent).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fccd1dc06aed`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.