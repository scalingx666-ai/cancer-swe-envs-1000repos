# Issue

**Title:** Make the single-sample WDL and SVShell run end to end: ConcatBaf, panel BAF, exit 141, EVIDENCE, sl_filter_args

## Description

### Why

On `main`, neither the single-sample WDL nor SVShell can finish a run on NA12878, and the single-sample run that does get far enough gives genomic-disorder (GD) calling a BAF matrix with one sample in it. This PR fixes each blocker and checks that all three pipeline flavors (single-sample WDL, sv-shell, joint/cohort WDL) still run. It's rebased on `main` at `c0314afa` (after #959).

### Changes

**Single-sample WDL** (`GATKSVPipelineSingleSample.wdl`)
- `ConcatBaf` called `/gatk/gatk`, which isn't in `sv_pipeline_docker` (exit 127). It now runs `java -jar ${GATK_JAR}` like the other `PrintSVEvidence` call sites, and passes the `--sequence-dictionary` that BAF files need.
- `ConcatBaf` listed only the case sample in `--sample-names`, so `PrintSVEvidence` dropped the whole reference panel. GD got a BAF matrix with 1 sample next to an RD matrix with 157. It now gets the case plus `ref_samples`.
- `IntegrateGDVcf` drops the case's hom-ref GD rows and adds `EVIDENCE=RD` to GD rows that lack it. Without that, `Final_VCF_Metrics` fails on records missing `EVIDENCE`.

**IntegrateGDVcf stays cohort-safe**
- The filter above only runs when the new optional `sample_id` input is set. Cohort runs leave it unset and get the integrator's VCF unchanged. Making it required, as an earlier commit here did, broke the cohort Terra config and would have filtered a multi-sample VCF on one sample's genotypes.

**Exit 141 (SIGPIPE) on header probes**
- `CondenseReadCounts` read the `@RG` sample name with `zcat | awk '... exit'` under `pipefail`. On large counts files zcat gets SIGPIPE and the task fails with 141 after already extracting the right value. Added `|| true`, matching its two sibling probes.
- Same guard on five other `zcat | head` header reads (`WGD`, `ConcatBeds`, `ConcatVapor`, `SplitCpxCtx`, `SplitRefBed`). These don't fail today because `pipefail` isn't on yet at that line; the guard keeps them safe if it is.

**SVShell**
- `filter_genotypes.sh` read `sl_filter_args` with a bare `jq -r`. `SVShell.wdl` drops empty inputs, so the key was missing and the script passed the string `null` to `apply_sl_filter.py`. That killed every SVShell NA12878 run at FilterGenotypes after ~44 h. It now reads `.sl_filter_args // ""`.
- `annotate_vcf.sh` always uses `par_bed` and the `external_af_*` inputs, but `SVShell.wdl` declared them optional, so a config without them would fail in AnnotateVcf (right after FilterGenotypes) on `null` paths. They're required now, so that config is rejected at launch instead.

**Other**
- `workspace.tsv.tmpl` for the single-sample Terra workspace referenced two GD keys the single-sample values don't define, so `build_inputs.py` skipped the whole table. Removed them.
- svtk keeps its `pkg_resources` import; the TODO in `svtk/__init__.py` now points at the two guards that keep it working (`setuptools<81` from #959 and the Dockerfile cap).

### Testing

Everything below ran on Terra or Cloud Build against this branch, with images built from it (`us.gcr.io/broad-dsde-methods/markw/gatk-sv/sv-pipeline:mwfix-bca30292`, `.../sv-shell:mwfix-77ddacf8`). The cohort runs used `main`'s images, since the branch's image changes are a comment. CI's local equivalents pass at `9acd9e2c`: miniwdl, womtool `validate.sh -t` (29/29 Terra JSONs), flake8.

| flavor | what ran | result |
|---|---|---|
| single-sample WDL | `GATKSVPipelineSingleSample`, NA12878 | Succeeded. BAF matrix 157 samples (was 1). Final VCF 9,467 records, record bodies identical to a run before the panel-BAF change; GD `cn_state` unchanged for every row |
| sv-shell | `SVShell`, NA12878, no call caching | Succeeded; earlier SVShell NA12878 runs on `main` and on #961 all failed. 9,207 records; QC flags the same 4 NA12878 size/BND ranges the WDL run flags |
| cohort | `IntegrateGDVcf`, 156-sample ref panel, `main` vs branch | Output records identical (md5 of record bodies) |
| cohort | `GatherBatchEvidence`, `EvidenceQC`, `MainVcfQc`, `RefineComplexVariants`, `AnnotateVcf` (with external AF), `VaporBatch` on ref-panel inputs | All succeeded; every changed task ran and exited 0, including `CondenseReadCounts` on all 156 samples |
| all | each guarded header probe on a 4M-line gzip, plus a control with `pipefail` forced on | Guarded lines rc 0 with unchanged values; controls rc 141 |

What this doesn't show: whether the full panel BAF changes calls for a sample where BAF is decisive (mosaic or partial CNVs). NA12878's GD calls didn't move; the GD probabilities did, by up to 0.43.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c0314afad9e0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.