# Issue

**Title:** Fix GUI help text silently missing for ~100 parameters (parse_docstring)

## Description

## Problem
`parsing.parse_docstring` extracted each `:param x:` description with a character-allowlist regex. Any description containing an unlisted character (`;`, `{}`, `|`, `&`, `~`, `^`, `$`, non-ASCII, ...) silently failed to match, so the GUI showed that parameter with an empty help tooltip (`<b>name:</b> <br>`). The same parser also dropped:
- the last `:param` of a paragraph (the lookahead required a following field line),
- params after a second blank line (only `split('\n\n')[1]` was scanned),
- params on accidentally indented lines (e.g. `normalize_to_tpm`, both limma-voom functions, `map_orthologs_phylomedb`, `tick_fontsize` on several plots),
and raised `IndexError` on a docstring with no blank line.

## Fix
``python
desc, _, params_str = docstring.partition('\n\n')
re.finditer(r'^[ \t]*:param ([a-zA-Z_0-9]+):([\s\S]*?)(?=^[ \t]*:.*:|\n\n|\Z)', params_str, re.MULTILINE)
``
Any text, non-greedily, up to the next reST field line (`:type x:`, `:return:`, `:Examples:`, ...), the end of its paragraph, or the end of the docstring. Return shape, the description, and the `'. '` -> `'. \n'` replacement are unchanged.

**Back-compat:** every parameter that parsed before produces byte-identical text. A regression test compares the new parser against a verbatim copy of the old one over every GUI-exposed function (>1000 params compared). I also diffed the full output of all public functions before and after: the only changed texts come from the docstring fixes below.

**HTML:** the text still goes into the HelpButton's rich-text tooltip unescaped, as before. None of the newly surfaced texts contain `<`, `>` or `&`.

## Docstring fixes surfaced by the new contract test
- `filter_by_go_annotations` (`Filter` and `FeatureSet`): `go_ids` had no help text. Added it.
- `bowtie2_align_paired_end`: `mate_orientations`, `allow_individual_alignment`, `allow_disconcordant_alignment` had no help text, and the latter two had truncated `:type` lines. Added both.
- `filter_by_go_annotations` / `filter_by_kegg_annotations`: a `param organism:` typo (missing leading colon) meant organism's help was appended to `mode`'s help. Fixed.
- `plot_expression`: the missing blank line after the description meant every param was swallowed into the function description. Fixed.

## Also fixed (found by the clean-context review)
- `bowtie2_align_paired_end(allow_disconcordant_alignment=False)` passed bowtie2 the misspelled option `--no-discorcordant`; it now passes `--no-discordant`. The test expectations that encoded the typo are corrected. Noted in `HISTORY.rst`.

## Numbers (measured on `development` at 485e8ce0, contract test logic, all public methods of Filter/CountFilter/DESeqFilter/FoldChangeFilter/FeatureSet/RankedSet + public `fastq`/`enrichment` functions)
- `development`: **177 of 1472** `:param` lines had no help text in the GUI (109 unique function definitions/params; the rest are inherited copies).
- this branch: **0 of 1484**.

## Tests
- New in `tests/test_parsing.py`: unit tests (special characters `; {} | ~ ^ $ & \ µ —  < >`, multi-line and backslash-continued descriptions, last param before `:return:`/`:rtype:`/`:Examples:`/a blank line/end of string, params in later paragraphs, no params section), real-function snapshots, the old-vs-new back-compat test, and a contract test that every `:param` of every GUI-exposed function gets non-empty help text.
- `pytest tests/test_parsing.py tests/test_fastq.py -p no:randomly` (after rebasing on the latest `development`): 365 passed.
- `pytest tests/test_gui_widgets.py tests/test_gui_windows.py -p no:randomly`: 526 passed.
- `pytest tests/test_gui.py -p no:randomly`: 445 passed, 6 setup errors (`KeyError: 'gui_stylesheet'` and similar) on a set of tests that changed between runs. Rerunning the errored tests on their own: all passed. These are the known shared-environment/Qt flakiness, not related to this change.

## GUI screenshots
Before/after renders of the help tooltip are posted in a comment below.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

https://claude.ai/code/session_0123vgnypTFGejWb1hprKoAS

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `72a8b57e710e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.