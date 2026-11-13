# Issue

**Title:** Raise TypeError on unknown GoSubDag and GOEnrichmentStudy keywords

## Description

.

## Problem
`GoSubDag` and `GOEnrichmentStudy` accept `**kws` and silently ignore keys they don't read. In #304, `relationship=rels` (missing the "s") was ignored:
- `GoSubDag` found 4 ancestors of GO:0019222 instead of 6;
- `GOEnrichmentStudy(relationship=…)` left `relationships=None`, so it propagated counts over `is_a` only, which changes enrichment results without any warning.

## Fix
- **New `chk_kwargs` in `gosubdag/utils.py`:** raises `TypeError` on an unknown keyword, the way Python does, and suggests the closest valid name:
  `GoSubDag() got an unexpected keyword argument 'relationship'. Did you mean 'relationships'?`
- **Accepted keywords:** each class lists the keys it and its helpers read (`kws_ok`). `GOEnrichmentStudy` also accepts algorithm-named keys such as `elim_cutoff`.

## Callers passing keys that nothing read
I found these by scanning every `GoSubDag` / `GOEnrichmentStudy` call in `goatools/`, `tests/` and the notebooks:
- **`plt_goids`** forwarded plot options (`mark_alt_id`, `title`, …) to `GoSubDag`. It now passes only `GoSubDag`'s own keys. I checked that it renders with plot-only options.
- **`plotobj._get_pltdag_path_hdr`** passed `dst_srcs_list` to `GoSubDag`, which never used it. Neither does `GoSubDagPlot`, so the "pruned" grouping plots have never pruned edges. Removing the argument changes nothing; wiring the pruning up properly is a separate fix.
- **`find_enrichment`** passed `remove_goids`, left over from disabled "BROAD" code. I removed that, along with the matching commented-out lines in `GOEnrichmentStudy`.

## Tests
- **New `tests/test_i304_unknown_kwargs.py`**, added to `CI_TESTS`: typos raise with the right hint, and valid calls work, including `elim_cutoff`. Both tests fail on `main`.
- **CI subset:** 200 passed, 12 skipped.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_01YaTHwoZmywheAEUdp4zJtb

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0f4999cec94b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.