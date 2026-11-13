# Issue

**Title:** Guideline updates 2026-09-23: biorxiv, cell, cell_genomics, cell_systems, iclr_2027, plos_compbio, science_immunology, s

## Description

Automated guideline check of 2026-09-23 (`scripts/update_guidelines.py`). Each venue below had a guideline page that changed, moved, or could not be vouched for; an agent re-read it and updated the entry. **Please check every rule change against the linked pages before merging** -- merging publishes the data to installed copies.

### `biorxiv` — re-read, no rule changed
No change: bioRxiv page diffs are heading-case only; every requirement is unchanged.

- changed: https://www.biorxiv.org/submit-a-manuscript
- changed: https://www.biorxiv.org/about-biorxiv

- `submit-a-manuscript`: the only differences are section headings going from upper case to sentence case (e.g. "SUBMISSION FORMAT" -> "Submission format"). The body text is identical. Formats (PDF, or Word plus separate figure files), the incompatible figure formats (PICT, Bitmap, Excel, PSD), LaTeX-to-PDF conversion, supplementary material, distribution licenses, article categories and revisions all match the entry.
- `about-biorxiv`: the only differences are three headings changing case ("Affiliates", "Frequently Asked Questions", "Contact bioRxiv"). No requirement is affected.
- `about/FAQ` was unchanged and I did not need it.
- I made no edit to `paperpush/manuscript_requirements.json`. `$aliases` covers manuscript section heading wording, not the venue's page headings, so it needs no change. `source_urls` are still accurate.

### `cell` — updated
Repoint cell's moved STAR authors guide URL in source_urls; no rules changed

- gone: https://www.cell.com/star-authors-guide

- `source_urls`: `https://www.cell.com/star-authors-guide` (404) -> `https://www.cell.com/information-for-authors/star-authors-guide`. A web search found the new location, and I read the page through `check_guidelines.py --text`.
- The moved page says the same as the entry. STAR Methods is not needed at submission, and the handling editor formats it after acceptance. The key resources table comes from a Word template or webform. STAR Methods text and the key resources table are not supplemental information. So no requirement values changed.
- The same dead URL is also in two other venues' `source_urls`, at about lines 2047 and 2316. I left those alone because the task is limited to the `cell` entry. They probably need the same fix.
- None of the other cell pages were listed as changed, so I did not re-audit them.

### `cell_genomics` — updated
Rename AI-declaration heading and repoint moved STAR guide URL for cell_genomics

- changed: https://www.cell.com/pb-assets/journals/EM/MasterFFCs/XGENFFC-1750589326387.pdf
- gone: https://www.cell.com/star-authors-guide

- Final File Checklist PDF diff: almost entirely whitespace/typo fixes; no limits or requirements changed.
- One wording change: AI declaration section heading `Declaration of Generative AI and AI-assisted technologies in the writing process` -> `Declaration of generative AI and AI-assisted technologies in the manuscript preparation process`. Updated the statements note (source: XGENFFC checklist PDF; other Cell Genomics pages already use the new heading).
- `source_urls`: `https://www.cell.com/star-authors-guide` (404) -> `https://www.cell.com/information-for-authors/star-authors-guide`. I did not re-fetch the moved page; I reused the location that the recent `cell` entry commit (fef8337) had found and read.
- The same dead URL is still in another venue's `source_urls` (about line 2047), and the old AI heading is still in other venues' notes (lines 1933, 2204, 5065). I left those alone, as the task is limited to `cell_genomics`.
- `retrieved` left untouched.

Could not be verified:
- Moved STAR authors guide page: relied on the earlier cell commit's finding rather than re-fetching it myself.
- JSON validity: I could not run a parser (command was blocked); the two edits were plain string replacements inside existing strings.

### `cell_systems` — updated
Rename Cell Systems AI-declaration heading; repoint moved STAR guide URL

- changed: https://www.cell.com/pb-assets/journals/EM/MasterFFCs/CELSFFC-1766175470697.pdf
- gone: https://www.cell.com/star-authors-guide

- Final File Checklist diff is otherwise whitespace/line-wrap only; every limit and requirement is unchanged (Report/Article/Brief Report item counts, section order, etc.).
- AI declaration heading: 'Declaration of Generative AI and AI-assisted technologies in the writing process' -> 'Declaration of generative AI and AI-assisted technologies in the manuscript preparation process' (`statements.notes`; Final File Checklist PDF). Still required only if AI was used in writing.
- `$aliases.sections.ai_use`: added the new heading; kept the old one.
- `source_urls`: `https://www.cell.com/star-authors-guide` (404) -> `https://www.cell.com/information-for-authors/star-authors-guide`. I fetched the new page and it loads, with the STAR Methods author guide content.
- Flag: other venues' notes still use the old AI heading (about lines 1933 and 5065). I left them alone because they are outside this task.

### `iclr_2027` — re-read, no rule changed
Leave iclr_2027 unchanged: diffs only drop the expired abstract-deadline countdown widget

- changed: https://iclr.cc/Conferences/2027/AuthorGuidelines
- changed: https://iclr.cc/Conferences/2027/CallForPapers

- **AuthorGuidelines** (https://iclr.cc/Conferences/2027/AuthorGuidelines): the only diff is "Sep 18, 2026 11:59 PM AOE or <countdown>" becoming "Sep 18, 2026 AOE" in two sentences. The abstract deadline passed on Sep 18, so the site removed the live countdown and the time-of-day text. The date and AOE timezone are unchanged. No page limit, format, statement, or policy text changed.
- **CallForPapers** (https://iclr.cc/Conferences/2027/CallForPapers): same single change on the "Abstract deadline" key-dates line. The paper deadline (Sep 25, 2026 11:59 PM AOE), reviews-released, discussion, and decision dates are unchanged.
- **Entry check**: the entry's deadlines note already records "abstract deadline Sep 18, 2026 11:59 PM AOE", which is what the page still means (AOE deadlines are end of day, and the key-dates header says all times are UTC-12h). No rule differs from the pages, so no edit was made.
- **Blog post** (https://blog.iclr.cc/2026/09/02/submission-policies-for-iclr-2027/): unchanged; nothing in it contradicts the entry.
- `source_urls` remain accurate; no page moved or disappeared.

### `plos_compbio` — re-read, no rule changed
Leave plos_compbio unchanged: only the Acknowledgments exclusion wording changed, no tracked rule

- changed: https://journals.plos.org/ploscompbiol/s/submission-guidelines

- **Only diff** on https://journals.plos.org/ploscompbiol/s/submission-guidelines: the Acknowledgments paragraph changed from "do not include editors or peer reviewers—named or unnamed" to "Per PLOS policy ... do not include editors or PLOS staff—named or unnamed".
- **Entry impact: none.** The `plos_compbio` entry lists `acknowledgements` only as an optional statement and records no rule about excluding editors, reviewers, or staff from it, so there is nothing to update. Adding a new note for this would go beyond the "record only what changed in a tracked rule" scope.
- **Every other rule** on the page (title lengths, abstract, Author Summary, sections, statements, references, cover letter) is unchanged per the diff.
- **Other six pages** (figures, tables, supporting-information, latex, journal-information, other-article-types) are reported unchanged; no contradiction with the entry was checked for beyond the diff since nothing in scope moved.
- `source_urls` remain accurate; no page moved or disappeared.

### `science_immunology` — re-read, no rule changed
Leave science_immunology unchanged: diff only recases a reporting-guidelines table header

- changed: https://www.science.org/content/page/sciimmunol-instructions-research-articles-initial-submission-new

- **Changed page** (sciimmunol-instructions-research-articles-initial-submission-new): the sole diff is the Reporting Guidelines table header changing from "TYPE OF STUDY GUIDELINES" to "Type of Study GUIDELINES". The rows beneath it (ARRIVE, REMARK, STARD, MOOSE, PRISMA, STROBE, STREGA, BRISQ, etc.) and every limit, format, section, and statement rule on the page are identical to the text the entry was written from.
- **Rules compared**: no word/figure/reference limits, title length, abstract length, file format, or required sections or statements differ from what the entry records, so no rule changed.
- **Other pages** (information-authors, science-journals-editorial-policies): reported unchanged; not re-read since nothing in the diff pointed at them.
- **source_urls**: all three pages still resolve at the recorded addresses; no change needed.

### `science_translational_medicine` — re-read, no rule changed
Leave science_translational_medicine unchanged: diff only recases a reporting-guidelines table header

- changed: https://www.science.org/content/page/stm-instructions-research-articles-initial-submission

- Changed page (stm-instructions-research-articles-initial-submission): the only diff is the table header "TYPE OF STUDY GUIDELINES" -> "Type of Study GUIDELINES" in the Reporting Guidelines section. The table contents (ARRIVE, REMARK, STARD, ...) and all word/figure/reference limits, required sections, statements, title-page items, figure specs, and file formats are unchanged.
- The entry records no rule tied to that header, so no rule, note, alias, or source_url needed changing.
- Context pages (stm-information-authors, science-journals-editorial-policies) are reported unchanged and were not re-audited beyond the diff scope.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `3c597dd0c04c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.