# Issue

**Title:** Release 4.0.0 - Reviewer 2 suggestions

## Description

<!--
# nf-core/raredisease pull request

Many thanks for contributing to nf-core/raredisease!

Please fill in the appropriate checklist below (delete whatever is not relevant).
These are the most common things requested on pull requests (PRs).

Remember that PRs should be made against the dev branch, unless you're preparing a pipeline release.

Learn more about contributing: [CONTRIBUTING.md](https://github.com/nf-core/raredisease/tree/master/.github/CONTRIBUTING.md)
-->

This PR addresses the reviewer comments on 

I haven't addressed one comment yet. . Full tests on AWS have not yet been set up for this pipeline, so addressing the comment now would still result in a failing test. Since the airrflow PR is also still unmerged, I can revisit this once either the template is fixed or the full tests are set up for this pipeline.

## PR checklist

- [ ] This comment contains a description of changes (with reason).
- [ ] If you've fixed a bug or added code that should be tested, add tests!
- [ ] If you've added a new tool - have you followed the pipeline conventions in the [contribution docs](https://github.com/nf-core/raredisease/tree/master/.github/CONTRIBUTING.md)
- [ ] If necessary, also make a PR on the nf-core/raredisease _branch_ on the [nf-core/test-datasets](https://github.com/nf-core/test-datasets) repository.
- [ ] Make sure your code lints (`nf-core pipelines lint`).
- [ ] Ensure the test suite passes (`nextflow run . -profile test,docker --outdir <OUTDIR>`).
- [ ] Ensure the test suite passes (`nextflow run . -profile test_singleton,docker --outdir <OUTDIR>`).
- [ ] Check for unexpected warnings in debug mode (`nextflow run . -profile debug,test,docker --outdir <OUTDIR>`).
- [ ] Usage Documentation in `docs/usage.md` is updated.
- [ ] Output Documentation in `docs/output.md` is updated.
- [ ] `CHANGELOG.md` is updated.
- [ ] `README.md` is updated (including new tool citations and authors/contributors).

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `e972dbde1aba`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.