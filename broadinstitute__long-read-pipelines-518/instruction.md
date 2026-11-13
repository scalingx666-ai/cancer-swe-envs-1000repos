# Issue

**Title:** Add HmmIBD IBD-inference pipeline + standalone FilterVcfForHmmIBD workflow

## Description

Adds an HmmIBD pipeline that infers identity-by-descent from a VCF/BCF by pre-filtering with bcftools and running hmmibd-rs (the Rust reimplementation of hmmIBD), plus a standalone
FilterVcfForHmmIBD workflow so the filtration step can be run (and its output format chosen) on its own. Includes a new lr-hmmibd-rs Docker image. All new files; nothing existing is
modified.

- wdl/pipelines/TechAgnostic/TertiaryAnalysis/HmmIBD.wdl — end-to-end pipeline: optional filtration → hmmibd-rs.
- wdl/pipelines/TechAgnostic/TertiaryAnalysis/FilterVcfForHmmIBD.wdl — standalone filtration workflow with configurable output_format: bcf (default), vcf, or hmmibd_table (the hmmibd-rs
text genotype table + matching allele-freq table).
- wdl/tasks/TertiaryAnalysis/HmmIBDTasks.wdl — tasks: FilterVcfForHmmIBD, HmmIBDrs, BcfToVcf, BcfToSampleTable.
- docker/lr-hmmibd-rs/ — Dockerfile + Makefile for hmmibd-rs (includes procps so the runtime free preamble works; LABEL maintainer).
- .dockstore.yml — registers HmmIBD and FilterVcfForHmmIBD.

Filtration knobs (FilterVcfForHmmIBD)

Masks low-depth genotypes (min_depth), recomputes AN/AC/AF (optionally per-population via populations_file), trims unrepresented alleles/sites, and strips heavy FORMAT/INFO (e.g. PL) early
for ~3× speedup on cohort VCFs. Configurable: variant_types (snps/indels/both), biallelic_only, split_multiallelics, max_variants (even genome-wide thinning), keep_original_af
(+rename_annots_tsv), and free-form extra_args (applied as a separate bcftools view pass so user -i/-e filters don't collide with the built-in include).
- mask_gq0_genotypes (default false): also null GQ=0 genotypes. Reproduces the GATK fix for #7792 () / #8741
() (pre-4.6.0.0 GenotypeGVCFs / GnarlyGenotyper emit no/low-confidence hom-refs as 0/0:GQ=0 instead of ./.), catching GQ0 calls the depth
mask misses.

hmmibd-rs (HmmIBDrs)

Every hmmibd-rs parameter is exposed with its upstream default (rec-rate/--genome, eps, min-inform, min/max-discord, min-snp-sep, fit thresholds, max-all, k-rec-max, buffers, filt-*,
par-mode, threads, bcf-read-mode). Output modes are honored and are mutually exclusive: normal HMM run → ibd_segments + ibd_fraction; --suppress-frac → segments only;
--bcf-to-bin-file[-by-chromosome] → binary_genotypes only (HMM skipped). from_bcf toggle lets it read a BCF/VCF (--from-bcf) or a pre-built text genotype table.

Pipeline wiring (HmmIBD)

- run_filtration (default true): call the FilterVcfForHmmIBD subworkflow first; otherwise feed input_vcf straight to hmmibd-rs.
- hmmibd_input_format (bcf/vcf/hmmibd_table): selects the read mode when filtration is skipped.
- Filtration knobs (incl. mask_gq0_genotypes, filter_extra_args) are plumbed through.

Outputs: ibd_segments, ibd_fraction, binary_genotypes, filtered_bcf (+ standalone filter workflow: filtered_bcf/filtered_vcf or sample_gt_table/sample_freq_table).

Validation

womtool validate and miniwdl check --strict pass on both pipelines (command blocks shellcheck-clean). Filtration and table-conversion logic smoke-tested with bcftools on a small Pf7 BCF.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `45c29af54297`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.