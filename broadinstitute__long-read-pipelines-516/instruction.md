# Issue

**Title:** BroadOnPrem pipeline 1: make VQSR best-effort (non-fatal)

## Description

GATK VQSR hard-fails on small callsets (the INDEL negative model: "No data found"), which failed the whole single-sample align+call workflow. Apply the "VQSR optional" runbook so VQSR is attempted unchanged but, on failure, the workflow still succeeds and delivers the gVCF and raw VCF; only the recalibrated VCF is omitted.

- New task VariantRecalibratorBestEffort: byte-identical GATK commands to VariantRecalibrator, but with -e off, each gatk call guarded, partial VQSLOD outputs removed on failure (all-or-nothing), status written to vqsr_ok.txt, exit 0. Outputs: Boolean vqsr_ok + File? vcf.
- Pipeline 1 calls the best-effort task; the SortCompressIndex consumer of the recalibrated VCF is gated on vqsr_ok (inputs via select_first).
- Workflow outputs: recalibrated_vcf / _index are now File?; a Boolean vqsr_succeeded is exposed. raw_vcf and gvcf stay required (upstream of VQSR).

The shared VariantRecalibrator task and pipeline 2 are untouched (a new task avoids changing pipeline 2's required-output contract). womtool + miniwdl clean.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ae9a6f58b09e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.