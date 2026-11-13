# Issue

**Title:** Permitting console users to specify fork and assembly; minor bug fixes at the VEP stage

## Description

Feature changes:
- Allows console mode users to use VEP in native GRCh37 mode. This includes the following edits:
  - Adding the `-A/ --assembly` argument, defaulting to `'GRCh38'`, that allows the user to specify the genome assembly during VEP;
  - The long form of the `-g` argument is changed to `--liftOver` to avoid confusion as for its purpose;
  - The assembly used in the VCF input is only checked in the webserver mode, per @ambj 's suggestions.
- Adding the argument `-F/--fork` with a default of 1 to control the number of forks used in VEP. The previous hard-coded default of 5 may be excessive in some configurations.

Bug fixes:
- VEP may introduce spaces between the colon and the chromosomal location in the `Location` field, so `build_vep_info` is changed to ensure all output lines were split correctly.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `08c167732e2e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.