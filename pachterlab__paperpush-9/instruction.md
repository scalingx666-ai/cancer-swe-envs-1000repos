# Issue

**Title:** Guideline updates 2026-11-01: arxiv, biorxiv, bmc_bioinformatics, cell_systems, combinatorica, cvpr_2027, discrete_mathe

## Description

Automated guideline check of 2026-11-01 (`scripts/update_guidelines.py`). Each venue below had a guideline page that changed, moved, or could not be vouched for; an agent re-read it and updated the entry. **Please check every rule change against the linked pages before merging** -- merging publishes the data to installed copies.

### `arxiv` — re-read, no rule changed
No edit: the arXiv change only rewords the troubleshooting list and keeps the case rule

- changed: https://info.arxiv.org/help/submit/index.html

- The only change on https://info.arxiv.org/help/submit/index.html is in its list of common compile errors. "five most common mistakes" became "four", and the separate "File-name upper/lower-case mismatch" item was removed.
- No rule changed. The same page still says "File names and extensions are also case sensitive on our system… internal file references, such as LaTeX figure inclusion commands, [must] match case exactly" (line 38). The remaining list item, "Missing, misnamed, or local complete paths to figure files", also says "arXiv's file system is case sensitive" (line 75). So the entry's note about case-sensitive file names is still correct.
- The mixed-figure-format item in that list is unchanged and still matches `figures.notes`.
- None of the unchanged context pages (submit_tex, sizes, submit_pdf, prep) was checked against the entry, so this does not confirm the entry is free of contradictions with them.
- Nothing was edited and `source_urls` was not changed.

Could not be verified:
- The unchanged context pages (submit_tex.html, sizes.html, submit_pdf.html, prep.html) were not read or compared against the entry, so contradictions on those pages would not have been caught.

### `biorxiv` — re-read, no rule changed
No edit: two journals left the transfer list and a new FAQ answer repeats existing rules

- changed: https://www.biorxiv.org/submit-a-manuscript
- changed: https://www.biorxiv.org/about/FAQ
- changed: https://www.biorxiv.org/about-biorxiv

- https://www.biorxiv.org/submit-a-manuscript and https://www.biorxiv.org/about-biorxiv: *Diabetologia* and *Pathogens and Immunity* were removed from the list of journals that take bioRxiv transfers. The entry doesn't record that list, so no rule changes.
- https://www.biorxiv.org/about/FAQ: new answer to "How do I submit to bioRxiv?". It says the simplest upload is one PDF with the text, tables and figures, with supplemental data as separate files, plus license selection and confirming co-author approval. The entry already records the combined-PDF option, separate supplements and the license choices, so no rule changes.
- https://www.biorxiv.org/about/FAQ: the question count went from 49 to 50 and the link to a more detailed submission FAQ was removed. Navigation only, no requirement affected.
- `source_urls` unchanged: all three pages still load.

Could not be verified:
- Only the changed parts of the three source pages were checked, as scoped. Unchanged sections were not re-checked against the entry.

### `bmc_bioinformatics` — re-read, no rule changed
No edit: the only change is a new pointer to next year's APC list

- changed: https://bmcbioinformatics.biomedcentral.com/submission-guidelines

- The only change on https://bmcbioinformatics.biomedcentral.com/submission-guidelines is one new sentence: "For information about the APC applicable for articles accepted for publication next year, please see our journal lists." It points readers to pricing information and doesn't change any submission requirement.
- The current APC stated on the page is still £2290.00 GBP / $3090.00 USD / €2590.00 EUR, with the country-tiered pricing pilot. That matches the entry's existing note, so the note stays as it is.
- The other article-type pages didn't change, so I didn't re-audit them. No rule, note or `source_urls` entry needed changing.

Could not be verified:
- Next year's APC amount: the new sentence only links to Springer Nature's journal lists and gives no figure, so I didn't record one (it's informational and not a submission-format rule).

### `cell_systems` — re-read, no rule changed
No edit: the only change drops 'MP4' from a STAR Protocols video note, not Cell Systems

- changed: https://www.cell.com/cell-systems/information-for-authors/final-submission
- unreadable: https://www.cell.com/cell-systems/information-for-authors
- unreadable: https://www.cell.com/cell-systems/information-for-authors/article-types
- unreadable: https://www.cell.com/cell-systems/information-for-authors/submit-manuscript
- unreadable: https://www.cell.com/cell-systems/information-for-authors/revise-manuscript
- unreadable: https://www.cell.com/information-for-authors/figure-guidelines

- The only change on the final-submission page is in a note about a different journal, STAR Protocols. The note used to say its videos "must be in landscape mode and in MP4 format". It now says only "must be in landscape".
- The `cell_systems` entry records nothing about STAR Protocols videos, so no rule is affected.
- The `.mp4` value in `supplementary.formats` comes from the shared supplemental-information page, which is unchanged and still says "Video files (.mp4 preferred)". It stays as it is.
- `source_urls` are still accurate.

### `combinatorica` — re-read, no rule changed
No edit: only the instructions PDF's listed size changed (115 kB to 258 kB)

- changed: https://link.springer.com/journal/493/submission-guidelines

- The only change on https://link.springer.com/journal/493/submission-guidelines is the size shown for the "Instructions for authors" download, which went from 115 kB to 258 kB. No requirement text on the page changed.
- I re-read the recorded PDF (…/95445_1085900_493_CCA_Instructions_to_authors_20240627.pdf) with check_guidelines.py. It is still online and says the same as the entry: EditFlow submission, a 30-page limit (11 pt LaTeX, US Letter, 1-inch margins), a brief abstract, double Arabic numbering, TeX/LaTeX for the final version, each figure as a separate EPS or vector PDF file that still reads in grayscale, affiliation and email for each author, a running head of at most 35 characters, and primary and secondary MSC codes.
- I changed no rules and left `source_urls` as they were.

Could not be verified:
- The submission-guidelines page now lists a 258 kB PDF, but I couldn't confirm that its link still points to the recorded 20240627 PDF. WebFetch got an idp.springer.com auth redirect, and fetching the raw HTML to read the link was blocked. If Springer has posted a new PDF at a new URL, I haven't read it.
- Ethics & disclosures page: unchanged, so I didn't re-check it.

### `cvpr_2027` — re-read, no rule changed
No edit: the supplementary deadline gained a time (11:59 PM AOE), but the date is unchanged

- changed: https://cvpr.thecvf.com/Conferences/2027/CallForPapers

- CallForPapers: the supplementary materials deadline changed from "Nov 23, 2026 AOE" to "Nov 23, 2026 11:59 PM AOE". The entry's note "due Nov 23, 2026" is still accurate, so no rule changed.
- No other lines changed on the CallForPapers page, and the AuthorGuidelines page did not change.

### `discrete_mathematics` — re-read, no rule changed
No edit: the only change rewords the open-access license-options sentence

- changed: https://www.sciencedirect.com/journal/discrete-mathematics/publish/guide-for-authors

- The only change to the guide for authors is in the "License options" paragraph: a comma was removed and "We advise that you review these options" became "Review these options". The meaning is the same.
- The entry records no rule about license choice, which is the author's own policy decision. Every recorded requirement still matches the guide: article types, keywords, statements, figures, references and supplementary material.
- The other source pages have not changed, so they were not checked again.

### `genome_biology` — re-read, no rule changed
No edit: the only change adds a pointer to next year's APC list; current APCs unchanged

- changed: https://genomebiology.biomedcentral.com/submission-guidelines

- https://genomebiology.biomedcentral.com/submission-guidelines: the only change in the diff is one new sentence, "For information about the APC applicable for articles accepted for publication next year, please see our journal lists."
- This is about fees and points to another page. It changes no formatting or submission rule.
- The current APCs on the page are still £3790/$5690/€4690, and £2850/$4280/€3520 for a Brief Report. These match the entry's `notes`, so no rule changed and the entry was left as it was.
- The other article-type pages were unchanged and were not re-checked.

### `genome_medicine` — re-read, no rule changed
No edit: both diffs only change homepage sidebar (calls for papers, latest articles)

- changed: https://genomemedicine.biomedcentral.com/submission-guidelines/preparing-your-manuscript/research
- changed: https://genomemedicine.biomedcentral.com/submission-guidelines/preparing-your-manuscript/method

- Research and Method page diffs: the only changes are the "Calls for papers" collections and deadlines and the "Latest articles" list. Neither touches a requirement, so no rule changed.
- Both URLs return the same text (same cache hash, 106 lines), and that text is the journal homepage, not the guideline content. `check_guidelines.py --text` on the Method URL gave the same homepage text. The live pages show no requirement text that differs from the entry, so nothing was changed. The entry's existing note already says the Research page was read from the Internet Archive because the live page was blocked.
- The main submission-guidelines page has not changed. Nothing in it contradicts the entry.
- `source_urls` stay as they are: the URLs still resolve, and no page has visibly moved.

Could not be verified:
- https://genomemedicine.biomedcentral.com/submission-guidelines/preparing-your-manuscript/research: the live fetch returns the journal homepage instead of the guideline text, so the rules recorded for Research articles (350-word structured abstract, 3-10 keywords, sections, figure and table rules) could not be checked again
- https://genomemedicine.biomedcentral.com/submission-guidelines/preparing-your-manuscript/method: the fetch (both the cached text and check_guidelines.py --text) returns the journal homepage, so the Method rules (100-word unstructured abstract, required sections) could not be checked again

### `jnm` — re-read, no rule changed
No edit: the diff only reorders the Clinical Trial Protocol row and Illustrated Post text

- changed: https://jnm.snmjournals.org/authors

- https://jnm.snmjournals.org/authors: the Clinical Trial Protocol table row moved and is now on one line, with the same values: 4,000 words, 350-word abstract, 40 references, 6 figures and tables combined. The entry already records all of these.
- The Illustrated Posts paragraph moved below the Clinical Trial Protocol paragraphs, and its text is the same. The entry's limits still match the page: 1 figure of up to 4 panels, no abstract, 5 references, 500 words.
- No rule changed, so the entry is unchanged.

### `medical_image_analysis` — re-read, no rule changed
No edit: the only change rewords the open-access license-options sentence

- changed: https://www.sciencedirect.com/journal/medical-image-analysis/publish/guide-for-authors

- The diff on the guide for authors (https://www.sciencedirect.com/journal/medical-image-analysis/publish/guide-for-authors) changes one sentence in "License options". "We advise that you review these options…" became "Review these options…", and a comma was dropped.
- The entry doesn't record license choices, and license is a `never`-role field that the author picks. So no requirement changed, and every rule in the entry still matches the guide.

### `medrxiv` — updated
Add teaching/instructive materials to medRxiv's out-of-scope content types

- changed: https://www.medrxiv.org/submit-a-manuscript
- changed: https://www.medrxiv.org/about/FAQ
- changed: https://www.medrxiv.org/content/about-medrxiv

- `notes[0]` (out-of-scope content types): the list "…laboratory protocols, theses, and manuscript components" now reads "…laboratory protocols, theses, manuscript components, and teaching/instructive materials". Source: https://www.medrxiv.org/about/FAQ, which adds "Teaching/instructive materials" to the list of article types that "are considered out of scope and will not be posted".
- No other edits:
  - The FAQ has a new "How do I submit to medRxiv?" answer. It repeats rules the entry already has: one PDF is preferred, supplements go in separate files, and funding, ethics and trial registration details are given at submission. It also bans participant-identifying details such as exact ages and photographs. The FAQ's unchanged "What information is considered identifying?" answer already said that, and the entry already records the photograph rule.
  - The FAQ's new table of contents and the obscured email addresses are layout changes only.
- https://www.medrxiv.org/submit-a-manuscript and https://www.medrxiv.org/content/about-medrxiv only drop Diabetologia from the list of partner journals. No requirement changed.
- `source_urls` stay the same.

Could not be verified:
- Could not confirm the JSON still parses: the parse command needed approval and did not run. The edit only changed text inside one existing string, so the structure is untouched.

### `nature` — updated
Matters Arising: first send the original authors a detailed summary of the issues

- changed: https://www.nature.com/nature/for-authors/matters-arising

- `article_types["Matters Arising"].manuscript.notes`, pre-submission contact rule: "Correspondents must first contact the authors of the original paper directly; a record of that correspondence must accompany the submission." -> "Correspondents must first send a detailed summary of the issues they wish to raise directly to the authors of the original paper; full details of that correspondence must accompany the submission." Source: https://www.nature.com/nature/for-authors/matters-arising, which now asks correspondents to "first send a detailed summary of the issues they wish to raise to the authors of the paper directly". Before, it only said to "contact" them.
- No other rule changed. The rest of the diff is the same, and the other pages were left alone as context. `source_urls` is unchanged.
- The edit only changes text inside one existing JSON string. I could not re-parse the file or view the git diff because both commands needed approval and were not run.

Could not be verified:
- The JSON was not re-parsed after the edit and the git diff was not viewed, because both commands needed approval; the change only swaps text inside one quoted string.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `2df710a3b401`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.