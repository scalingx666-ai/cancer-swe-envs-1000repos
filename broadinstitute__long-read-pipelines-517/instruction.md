# Issue

**Title:** P. falciparum variant-calling: small-genome benchmarking + Pf7 reimplementation pipelines

## Description

## Summary

Adds tooling to validate and benchmark short-read variant-calling pipelines on
small genomes (*Plasmodium falciparum*), plus robustness fixes to the Pf joint-
and single-sample callers. Three new workflows are registered in Dockstore; the
remaining changes harden existing Pf pipelines against small/low-variance-callset
failure modes surfaced while running the validation on Terra.

## What's included

### New: `BenchmarkVCFsSmall` (`wdl/pipelines/TechAgnostic/Utility/BenchmarkVCFsSmall.wdl`)
A cost-optimized truth/eval benchmark for small genomes.
- Stratified SNP/indel precision–recall via `rtg vcfeval`, with per-indel-length-bin
evaluation folded into the main stratifier scatter.
- Avoids the tabix/index crash on empty/sparse `SelectVariants` output by using
uncompressed `.vcf` intermediates and skipping the output index on the indel step.
- Emits a progress line per completed indel bin; keeps indel summary rows in
`bins.tsv` order for stable, diff-able output.

### New: Pf7 reimplementation pipelines (`wdl/pipelines/Z_One_Off_Analyses/`)
- `Pf7JointGenotyping.wdl` — cohort joint genotyping mirroring the Pf7 per-window
path (GenomicsDBImport → GenotypeGVCFs → excise padding → merge), interval
scatter/gather.
- `Pf7SingleSampleVariantCalling.wdl` — single-sample calling; VQSR step made
**optional/best-effort** so a small callset that underfills the model still
yields a gVCF and genotyped VCF instead of failing the workflow.

### Robustness fixes (Pf callers)
- **`Pf7JointGenotyping` — container swap:** `MakeIntervals` used GNU `split -d`
on an Alpine/BusyBox bcftools image (no `-d`), failing immediately. Switched the
shared `bcftools_docker` default to `us.gcr.io/broad-dsp-lrma/lr-basic` (Debian /
GNU coreutils; already used elsewhere in the workflow).
- **`Pf7JointGenotyping` — organellar contigs:** `MakeIntervals` tiled the full
reference `.fai`, so the apicoplast/mitochondrion contigs produced genotyping
windows that GenomicsDBImport rejects (mito is shorter than one padded window).
Added `Array[String] contigs_to_exclude = ["Pf3D7_API_v3","Pf3D7_MIT_v3"]`,
threaded into the tiling step. Nuclear-only joint calling; default preserves prior
behavior for other contigs.
- **Pf_Niare VQSR — `--max-gaussians` parameterized:** was hard-coded to 4 in the
`VariantRecalibrator{Snp,Indel}` tasks (`Pf_Niare_HaplotypeCaller.wdl`), giving no
way to back the SNP model off on small per-contig callsets that fail to converge
("insufficient variance"). Exposed `snp_max_gaussians` / `indel_max_gaussians`
(default 4) on `SRJointCallGVCFsWithGenomicsDB_Pf_Niare_VQSR` and
`SRWholeGenome_Pf_Niare_VQSR`, threaded to the recalibrator tasks.

## Dockstore
Registers `BenchmarkVCFsSmall`, `Pf7JointGenotyping`, and
`Pf7SingleSampleVariantCalling` in `.dockstore.yml` (task libraries unchanged).

## Validation
Every changed `.wdl` validated with **both** `womtool validate` (Cromwell source of
truth — all `Success!`) and `miniwdl check --strict` (no new warnings beyond
pre-existing `ls`/quoting shellcheck lint). Exercised end-to-end on the
`broad-firecloud-dsde-methods/malaria_variant_calling_validation` Terra workspace
across the pfcrosses, pfcrosses_v2, sr_fiddock, and niare2023 truth sets.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `7e0fd150dbc4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.