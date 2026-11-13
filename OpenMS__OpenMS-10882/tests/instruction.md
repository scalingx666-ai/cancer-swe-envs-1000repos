# Issue

**Title:** [FIX] ProSE: keep_termini decoys keep the cleavage residues of the search enzyme

## Description

## Description

With `decoy_method keep_termini`, ProSE now keeps in place the residues that the search enzyme's cleavage rule names, plus P. Before, it kept K, R and P for every enzyme. Decoys for non-tryptic enzymes now have the cleavage sites of their targets. Trypsin/P decoys are unchanged.

**Problem.** `keepTerminiDecoy` called `MRMDecoy::reversePeptideLight(segment, {}, true, true, "KRP")` for every enzyme. That fits Trypsin and Trypsin/P, but not Chymotrypsin. Chymotrypsin cuts after F, W, Y or L unless P follows, so an F/W/Y/L before P sits inside a segment. The reversal moved it, and it mostly became a new cleavage site in the decoy.

On the Percolator yeast database (6,734 proteins), the decoy parity report (`-Search:decoy_parity_report true`) found 5,183 decoys whose cleavage sites differed from their target's. ProSE warned about them. With up to two missed cleavages and 7–40 residues, those decoys had 2.4% more distinct peptides than the targets (942,066 vs 920,048). More decoy candidates tend to raise the estimated FDR.

**Change.** The residues kept in place come from the enzyme's cleavage regex (`keepTerminiFixedResidues()`): every residue letter it names, plus P.
- Trypsin, Trypsin/P: K, R, X, P. For Trypsin/P an X always ends a segment, so the decoys are those of `-Decoy:non_shuffle_pattern K,P,R`, as before.
- Chymotrypsin: F, Y, W, L, J, X, P.

Inside a segment, a residue then either stays in place or trades places with one the rule treats alike. So every rule of the ProteaseDB that tells residues apart only by the letters it names finds the target's sites in the decoy. The documentation of `decoy_method` and the decoy note of the ProSE tool (`src/topp/ProSE.cpp`) are updated.

**Effect** (yeast, `-Search:decoy_parity_report true`):

| Enzyme | Cleavage-site mismatches before | after | Decoy checksum (FNV-1a 64) |
|---|---|---|---|
| Chymotrypsin | 5,183 | 0 | changes |
| Trypsin/P | 0 | 0 | unchanged, `463bbd7cbc5c157` |
| Trypsin | 1 | 0 | changes for the one protein with an X before a P (YIL080W) |

Decoys taken from the database (`decoys auto` with decoys in it) are not affected.

**Tests.**
- The keep_termini test over all enzymes of the ProteaseDB now checks that every decoy has its target's cleavage sites, and that the Trypsin/P decoys equal those of "KRP". Without the fix it fails for the 13 enzymes with a "not before P" rule; with the fix it passes.
- New hand-written Chymotrypsin decoys.
- Debug build:
  - `ProSEAlgorithm_test` passes;
  - `ctest -R 'ProSE|DecoyDatabase'`: 274 of 274 pass.

**Context.** This came up in the ProSE paper benchmark. The benchmark databases hold ProSE's keep_termini decoys, so all engines search the same decoys, and the benchmark stays on the tag `prose-benchmark-2026-11`, which this PR does not change.

## Checklist
- [x] Make sure that you are listed in the AUTHORS file
- [x] I have commented my code, particularly in hard-to-understand areas
- [x] New and existing unit tests pass locally with my changes
- [x] Updated or added python bindings for changed or new classes (Tick if no updates were necessary.)

### AI use (see the [OpenMS AI Policy](https://openms.de/ai-policy/))
- [x] I have read the [OpenMS AI Policy](https://openms.de/ai-policy/), and I understand, have reviewed and tested every change in this PR and can explain it in my own words
- AI use in this PR (tick one):
  - [ ] None
  - [ ] Assisted (e.g. completion, suggestions, small edits); commits carry an `Assisted-by:` trailer
  - [x] Substantial (e.g. agentic tools wrote significant parts); commits carry a `Co-authored-by:` trailer, and the description above explains the design intent and rationale

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fbb25191d765`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.