# cancer-swe-envs-1000repos (1000-Repo Breadth Edition)

A large-scale SWE-style RL environment dataset built from merged pull requests
of 1000 cancer / oncology / cancer-genomics / biomedical open-source repositories,
generated with the Repo2RLEnv pr_diff pipeline and emitted in the Harbor task format.

- Target repositories: 1000
- Repositories with tasks: 660
- Total tasks: 1479
- Max tasks per repository: 3 (kept at most 3 by design)
- Repositories with zero yield: 340 (kept in the target list, never faked)

## What a task is

Each task rewinds a merged pull request to its base commit. The agent gets the PR
title and description (with leak patterns stripped) and must edit the repo to resolve
the issue; a 6-component weighted diff-similarity verifier compares its patch against
the merged diff (diff_similarity reward, plus an LLM judge required for the graded
verdict). Generation needs no Docker and no LLM; tasks ship a self-contained
python:3.12-slim inline Dockerfile so consumers rebuild from the recipe.

## How this edition was built

1. Candidate pool: 41 GitHub search queries across cancer / oncology / tumor /
   neoantigen / radiomics / TCGA / single-cell / variant-calling / immunotherapy /
   spatial-transcriptomics / medical-imaging topics plus name/description searches,
   merged and de-duplicated into 4172 unique repos;
   859 noise repos (awesome-lists / tutorials / course /
   science-fair / questionnaire / archived) removed.
2. Selection: strict superset of the earlier 100-repo edition (100
   seeds kept), then high-star / actively-maintained repos first. Star buckets:
   >=1000 63, 500-999 93, 200-499 276,
   100-199 369, 50-99 170, <50 29.
   Active since 2023: 856. Core cancer/oncology-tagged: 443.
3. Generation: concurrent repo2rlenv generate --pipeline pr_diff
   (limit=4, max_files_per_pr=15, min_loc_changed=2), rate-limit-aware with
   checkpoint resume. Zero-yield repos were retried with relaxed filters.
4. Task selection: per repo, ranked by reward_calibration.loc_changed descending,
   keeping at most 3 tasks.
5. Validation: repo2rlenv validate --deep --oracle (static structure +
   oracle-patch integrity). See BREADTH_NOTES.md.

## Repository distribution (top 15)

- 10XGenomics/HumanColonCancer_VisiumHD: 3
- 10XGenomics/vartrix: 3
- 3dmol/3Dmol.js: 3
- ACEnglish/truvari: 3
- AI-sandbox/gnomix: 3
- AIM-Harvard/SlicerRadiomics: 3
- AIM-Harvard/foundation-cancer-image-biomarker: 3
- ANTsX/ANTsPy: 3
- Acellera/moleculekit: 3
- Adibvafa/CodonTransformer: 3
- AlexsLemonade/refinebio: 3
- Azure-Samples/healthcare-agent-orchestrator: 3
- BMIRDS/deepslide: 3
- BenLangmead/bowtie2: 3
- BiaPyX/BiaPy: 3

## Layout

One directory per task, named owner__repo-<pr_number>. Each contains task.toml,
instruction.md, solution/patch.diff, environment/Dockerfile, and tests/ with
test.sh, verifier.py, capture.py, oracle.patch, instruction.md. manifest.json and
registry.json (Harbor-compatible) are added on Hugging Face by repo2rlenv push.

## Files

- README.md - this card
- BREADTH_NOTES.md - build notes, filtering logic, caveats
- repo_list_1000.txt - the full 1000-repo target list
- dataset_stats.json - per-repo task counts and summary
- zero_repos.txt - repos that yielded no usable PR (informational)

## Status / caveats

- Tasks are generation-stage / unverified: --deep --oracle proves static
  structure and oracle integrity, NOT real Harbor agent reward.
- A graded run requires an LLM judge key; harbor run --env docker requires a
  Docker daemon. Neither is needed to generate, statically validate, or publish.
- Earlier editions are preserved and published separately:
  cancer-swe-envs (14 repos / 135 tasks, deep) and
  cancer-swe-envs-100repos (100 repos / 210 tasks, breadth).
- License of each task follows its source repository; this dataset is a derived
  research artifact. Generated with Repo2RLEnv (Apache-2.0).
