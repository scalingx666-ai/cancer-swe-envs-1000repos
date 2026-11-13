# Issue

**Title:** Add GUI docstring pre-commit hook, pre-push format checks, and .gitattributes

## Description

This was meant to stack on #343, which has since been merged into `development`, so this PR targets `development` directly. It is developer tooling only: no GUI-visible change, and GUI help text is unchanged.

## 1. `check-gui-docstrings` pre-commit hook

- **Shared parser.** `parse_docstring`'s implementation now lives in a new stdlib-only module, `rnalysis/utils/docstring_parsing.py`. `rnalysis.utils.parsing.parse_docstring` delegates to it, so the GUI and the hook use one parser. Output is byte-identical: #343's legacy-equivalence test still passes, and a new test checks that both entry points agree on every GUI-exposed function.
- **Hook script.** `packaging/check_gui_docstrings.py` reads the code with `ast`. It never imports `rnalysis`; it loads the parser by file path, because the pre-commit env has no polars/numpy/PyQt.
- **Which files.** It runs on `rnalysis/filtering.py`, `enrichment.py` and `fastq.py` when they change. If the script or the parser changes, it checks all three.
- **What it flags,** each reported as `file:line: qualname: parameter 'x' <what's wrong>`:
  - `missing-help`: a signature parameter (not self/cls/*args/**kwargs) whose parsed help text is missing or empty.
  - `unknown-param`: a `:param x:` naming a parameter that isn't in the signature (a typo).
  - `malformed-field`: lines like `param x:`, `:param x` or `:param int x:` that the parser can't read.
  - `no-blank-line`: no blank line before the `:param` block, so the parser swallows it into the description.
  - `no-docstring`: a `@readable_name` function that has parameters but no docstring.
- **Registration.** Added to `.pre-commit-config.yaml` as a `repo: local` hook with `language: python`, no extra dependencies, and `files:` limited to the three modules plus the script and the parser.

**Static approximations** (documented at the top of the script):
- **Functions checked.** The set mirrors #343's contract test: public methods of `Filter`/`FeatureSet` and their subclasses, plus public module-level functions in `fastq`/`enrichment`. Functions in `EXCLUDED_FUNCS` are still checked.
- **Hidden parameters.** Methods skip `FuncTypeStack.EXCLUDED_PARAMS` (`backend`, `gui_mode`, `legacy_args`, `function_kwargs`). Module functions skip only `legacy_args`. Exclusions that are specific to one window are not mirrored.
- **Inherited docstrings.** Docstrings are looked up through base classes in the same file. Builtin bases such as `set` are checked directly. A method with no docstring whose class has some other external base is skipped, because its docstring may be inherited from there.
- **Undecorated methods.** `no-docstring` only fires for `@readable_name` functions.

**Baseline.** The current tree has 35 real, pre-existing gaps. They are listed in `KNOWN_ISSUES` so the hook passes today. A fixed entry is reported as stale, so the list can only shrink:
- `random_seed` is undocumented in `go_enrichment`, `kegg_enrichment`, `user_defined_enrichment` and `randomization_test`.
- `consistency_score_threshold` is undocumented in `map_orthologs_phylomedb`.
- `differential_expression_deseq2` is missing `scaling_factors` and `cooks_cutoff`.
- `split_by_percentile` is missing `interpolate`.
- `Filter.concatenate`, `Filter.histogram` and `fastq.create_bam_index` have no docstring.
- Stale `:param` lines name parameters that no longer exist: `biotype`/`biotype_ref_path` in two enrichment functions, `long_format` in `biotypes_from_gtf`, `learn_bias`/`seek_fusion_genes` in kallisto, `input_folder` in `fastq_to_sam_paired`, `new_sample_names` in `validate_sam`.
- The rest are in the script.

Fixing these changes visible help text, so they would need screenshots (rule 9) and were left for follow-ups.

## 2. Format checks on push

- **pre-push hook.** `default_install_hook_types: [pre-commit, pre-push]`: `pre-commit install` now also installs a pre-push hook. On push, every hook runs on the working-tree copies of the files changed since the remote branch. If a fixer hook changes a file, the push is aborted; commit the fix and push again. Existing clones need to run `pre-commit install` once more.
- **CI on push.** `.github/workflows/pre-commit.yml` now also runs on pushes to `development` and `master`, scoped to `event.before...sha`.
  - When `before` is all zeros (a new branch), or the old tip can't be fetched after a force-push, it checks only the pushed tip commit against its first parent.
  - `pull_request` behaviour is unchanged (same base/head SHAs).
- **Docs.** Updated CLAUDE.md, AGENTS.md (kept in sync), `.claude/workflows.md` and CONTRIBUTING.rst. CLAUDE.md's stale "not fully reformatted yet" note now matches the config: the sweep landed in #299.

## 3. `.gitattributes`

- **Rules:**
  - `* text=auto eol=lf`.
  - `-text` (no conversion) for `tests/test_files/**`, `rnalysis/data_files/r_templates/**` and `rnalysis/data_files/report_templates/**`.
  - Explicit `binary` for images, fonts, archives, BAM/bt2/idx, `.rnal`, and Sphinx `.doctree`/`.inv` files.
- **`git add --renormalize .` findings:**
  - No index blob contains CRLF. `git ls-files --eol` showed only `i/lf`, `i/-text` and `i/none` before the change, so the commit renormalizes nothing.
  - Running renormalize *after* adding the attributes staged CRLF versions of about 330 files under `tests/test_files` and the template dirs: with `-text`, a CRLF `autocrlf` working copy is stored as-is. None of that was committed.
- **Check after the change:** after deleting a tracked `.py` and running `git checkout --` on it, the file has 0 `\r`.
- **`.bat` files stay LF.** A `*.bat eol=crlf` rule would fight `mixed-line-ending --fix=lf`.
- **Maintainer action for existing Windows clones** (`core.autocrlf=true`): old CRLF working copies stay until files are re-checked out. On a clean tree, run `git rm -r --cached -q . && git reset --hard`, or re-clone. This is also in the `.gitattributes` header.
- **Watch the first Windows CI run.** Windows checkouts of fixtures are now LF instead of CRLF. `tests/__init__.py::are_dir_trees_equal` compares in a newline-tolerant way, and local Windows runs of the fixture-heavy modules pass.

## Tests
- Passed:
  - `tests/test_parsing.py`, `tests/test_check_gui_docstrings.py` (new, 30 tests), `tests/test_gitattributes.py` (new): 293 passed.
  - `tests/test_filtering.py` and `tests/test_fastq.py`: 611 passed.
  - `tests/test_differential_expression.py`, `tests/test_feature_counting.py`, `tests/test_api_docstrings.py` and `tests/test_io.py` (run together with the three modules above): 702 passed, 4 failed. All 4 failures are `test_io.py::test_run_subprocess`, which fails because the sandbox has no `%ComSpec%`; this PR doesn't touch it.
- `pre-commit run --from-ref origin/development --to-ref HEAD` and `pre-commit run check-gui-docstrings --all-files` both pass.
- Planting a `param n_clusters:` typo in `filtering.py` makes the hook fail with `rnalysis/filtering.py:5211: CountFilter.split_kmeans: parameter 'n_clusters' has a malformed ":param" line...`.
- Not run: the `push` trigger in a real GitHub run (the range-selection bash was tested locally for the fast-forward, new-branch and unreachable-tip cases), and the GUI/R test modules.
- An independent clean-context review was run, and its findings are addressed in the second commit.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_0123vgnypTFGejWb1hprKoAS

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `393fd9adaabd`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.