# Issue

**Title:** Require the GATK-SV ploidy table for GD calling

## Description

Companion to broadinstitute/gatk-sv-gd#2 (merged). Requires an `sv_pipeline_docker` built from this branch.

Replaces #963, which was mistakenly based on `mw_gd_external`.

## Problem

`CallGenomicDisorderCNVs` invokes `run_gd.sh` with no ploidy table, so the GD pipeline derives ploidy from median bin depth while `IntegrateGDVcf` encodes genotypes from GATK-SV's sex-assignment table. For a `sex=0` sample the two disagree on every allosome — depth sees one or two X chromosomes, the table says `chrX=0` — and integration dies:

```
ValueError: Detected GD call GD_Xp22.31_DEL_chrX_6537771_8156913/DEL has zero sample ploidy
```

## Changes

**`wdl/CallGenomicDisorderCNVs.wdl`** — new **required** `File ploidy_table` on workflow and task, passed to `run_gd.sh --ploidy-table`. Required rather than optional deliberately: an optional input lets batches keep drifting and the failure resurfaces later, far from its cause.

**`wdl/GATKSVPipelineSingleSample.wdl`** — passes `CreatePloidyTableFromPed.out`, the identical expression already supplied to `IntegrateGDVcf` as `ploidy_tables`. One file feeding both stages is the whole fix.

**`wdl/IntegrateGDVcf.wdl`** — the per-batch ploidy merge verifies headers match before concatenating. Mismatched contig columns previously appended rows that didn't line up with the header; with the companion PR's stricter parser that becomes a parse error, so this fails earlier with a clearer message.

**`dockerfiles/sv-pipeline/Dockerfile`** — pins `gatk-sv-gd` to `e16f9a5`, and caps setuptools (below).

**Input templates** — `ploidy_table` added to the cohort Terra config (`${this.ploidy_table}`, matching `GenotypeBatch.json.tmpl` on the same entity type) and to the test template.

## Separable commit: setuptools cap

`1f2aaff2` is unrelated to ploidy and fixes `main` on its own. sv-pipeline builds currently fail at `RUN svtk -h` with `ModuleNotFoundError: No module named 'pkg_resources'`: the base image ships setuptools 62.1.0, but installing gatk-sv-gd pulls torch/triton, which require `setuptools>=77.0.3` and now resolve to 84.0.0 — the release that removed `pkg_resources`. svtk/svtest/svqc console scripts still use `__import__('pkg_resources').require(...)`. Capping at `>=77.0.3,<81` satisfies triton and keeps `pkg_resources`.

Happy to split this out if you'd rather land it ahead of the ploidy work.

## Validation

Built `sv-pipeline:mw-gd-ploidy-table-a5ffd5` from this change set and ran both workflows on a sandbox clone of the joint-calling featured workspace (156-sample 1KGP cohort):

- **`CallGenomicDisorderCNVs` — Succeeded.** All 3744 sample/contig pairs recorded `ploidy_source=table`; chrX ploidy split 78/78 matching the sex assignment; 0 pairs discordant with depth; 32,760 call rows, 6 carriers across 5 GD sites.
- **`IntegrateGDVcf` — Succeeded.** 63,333 records, with GD annotations at 1q21.1, 15q11.2, 15q13.3, 16p13.3, 22q13.33 and others, mixing freshly emitted `_novel` GD records with in-place annotation of existing records. On chrX GD records `ECN` is 1 for 78 samples and 2 for 78. 8,814 `ECN=0` genotypes, all chrY in female samples, all no-calls.

Scope note: that cohort contains no `sex=0` samples and the GD table has no chrY loci, so neither `call`'s zero-ploidy skip nor `integrate`'s complete-cohort exemption ran in the cloud. Those paths are covered by the companion PR's unit tests and by a local spike test that zeroes two samples' allosomes and confirms their chrX spikes are not called while the same sample's chr22 spike still is.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fc014646fbd6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.