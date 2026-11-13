# Issue

**Title:** vcfwave: index Number=R INFO fields by allele, not by ALT (AT names the wrong allele)

## Description

> **Disclaimer:** this was prepared by Claude Code (an AI coding agent) on behalf of
> @cmdcolin, who has reviewed it. Everything below was reproduced and measured against
> a build rather than reasoned about — but please review it as you would any patch from
> a stranger.

## The bug

`vcfwave` pulls `AT` onto each decomposed record using `alt_index`, the 0-based index
into the ALT column. That's right for `AC` and `AF`, which are `Number=A`. `AT` is
`Number=R` — one entry per allele **including the reference at index 0**, so allele
*k* sits at index *k*, the same numbering `GT` uses.

| declaration | one value per | length | index of allele *k* |
|---|---|---|---|
| `Number=A` | ALT allele | `nALT` | `k - 1` |
| `Number=R` | allele incl. REF | `nALT + 1` | `k` |

So the current code lands one slot early, and also emits a single value where
`Number=R` requires one per allele.

## Reproducing

```
##INFO=<ID=AT,Number=R,Type=String,Description="Allele Traversal as path in graph">
##INFO=<ID=AC,Number=A,Type=Integer,Description="Allele count">
chr1  10  bub1  ACGTACGT  ACATACGT,ACGTAAGT,TCGTACGT  60  .  AT=>1>2>5,>1>3>5,>1>4>5,>1>6>5;AC=1,1,1  GT  1  2  3
```

```console
$ vcfwave -I 1000 min.vcf
chr1  10  bub1_1  A  T  AT=>1>4>5;...    # came from ALT3, got ALT2's traversal
chr1  12  bub1_2  G  A  AT=>1>2>5;...    # came from ALT1, got the REF's
chr1  15  bub1_3  C  A  AT=>1>3>5;...    # came from ALT2, got ALT1's
```

It happens on your own test data too: in `samples/10158243.vcf`, decomposed record
`>3655>3662_3` — the `AC=64` majority allele — comes from ALT1 and is written with
`AT[0]`, the reference's traversal.

It fails quietly. `AT[GT]` still returns a well-formed traversal string, just the
wrong allele's, so nothing downstream errors; and on a biallelic record a single
value looks like a plausible `Number=R` payload until you count it.

## The fix

Read `AT[0]` and `AT[alt_index + 1]`, emit both. `AT` is also part of the `ntag`
merge key that keeps identical primitives from different parent alleles apart, so
that moves to the ALT traversal too.

## What changed in the expectations

Regenerated `test/pytest/vcfwave.md` and the three `test/data/regression/vcfwave_*.vcf`
files. **Ignoring `AT` and the auto-assigned `_N` record-id suffix, the regression
outputs are unchanged** — `diff` reports 0 differing lines for `vcfwave_4` and
`vcfwave_5`. Specifically:

- same record counts (939 / 1934 / 3);
- total `AC` conserved (4740 / 23922 / 6);
- identical `AC`-vs-`GT` mismatch counts before and after (5 in `vcfwave_4`, 142 in
  `vcfwave_5` — pre-existing, neither introduced nor fixed here).

Most of the apparent diff is the `_N` suffixes moving: the merge map is keyed by a
string containing `AT`, so correcting `AT` changes its iteration order and hence which
group is emitted as `_1` vs `_3`. If that churn is unwelcome, keying the map on
`alt_index` instead would avoid it — say the word.

Inversions, which aren't decomposed, now pass their `AT` through unchanged rather than
being truncated to the reference entry.

## Scope

On a 150 kb slice of a pggb snarl VCF (6,344 records in): stock emits 1,115 records
with `AT` arity disagreeing with their allele count, patched emits 0, with identical
record counts and otherwise identical output.

`pggb -V ref:LEN` runs `vcfbub | vcfwave` and ships the result as its decomposed VCF,
so this affects every such callset.

## One judgement call

The values emitted still describe the **parent bubble's** paths. A primitive pulled
out of a bubble isn't itself a traversal — its REF is a substring of the parent REF,
matching part of the parent's reference path rather than the whole of it — and
`vcfwave` never sees the graph, so it can't re-derive a true sub-traversal.

I've written it the conformant way because it keeps `AT` readable by `GT` and keeps
existing consumers working. The alternative, which claims less, is to drop `AT` from
decomposed records entirely and put the source allele's traversal in its own
`Number=1` field. Happy to switch if you prefer that.

Separately and not addressed here: the wholesale `newvar.info = var.info` copy leaves
every *other* `Number=R`/`Number=A`/`Number=G` field at the parent's arity — a
user-defined `Number=R` field keeps all its parent values on a 2-allele record. Same
class as #225. I left it alone rather than guess at the right subsetting policy.

## Build

`cmake -DZIG=OFF -DWFA_GITMODULE=ON -Dpybind11_DIR=...`, gcc 15, against `v1.0.15`.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `b118a9bfd99b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.