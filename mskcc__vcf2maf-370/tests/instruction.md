# Issue

**Title:** fix: for SVs, use the main CHROM as a fallback for the END breakpoint chromosome

## Description

I was seeing an error similar to the one mentioned in the discussion of #326, the one right here:


Edited for brevity, the gist is this:
```
STATUS: Preprocessing input.vcf: split SV breakpoints before passing to VEP...
[...]
Use of uninitialized value in concatenation (.) or string at /path/to/bin/vcf2maf.pl line 336, <GEN0> line 7153.
[W::fai_get_val] Reference :715268-715268 not found in FASTA file, returning empty sequence
[W::fai_get_val] Reference :715268-715268 not found in FASTA file, returning empty sequence
[faidx] Failed to fetch sequence in :715268-715268
Use of uninitialized value in join or string at /path/to/bin/vcf2maf.pl line 338, <GEN0> line 7153.
[...]
STATUS: Pulling flanking reference bps for checks...
STATUS: Splitting loci into smaller chunks to run separately...
[W::fai_get_val] Reference :715267-715269 not found in FASTA file, returning empty sequence
[W::fai_get_val] Reference :715267-715269 not found in FASTA file, returning empty sequence
[faidx] Failed to fetch sequence in :715267-715269
[...]
ERROR: You're either using an outdated samtools, or --ref-fasta is not the same genome build as your --input-vcf. at /path/to/bin/vcf2maf.pl line 433.
```

So in this case, the chromosome field seems to be empty. And this is reflected in the intermediate `.split.vcf` file produced by `vcf2maf.pl`:
```
	715268	DUP00000603	G	<DUP>	.	.	END=715268
X	714908	DUP00000603	G	<DUP>	.	.	END=715268
```

So, the chromosome seems to get lost during the splitting of `SV` records, and I was able to track down the code where this happens. The previous code assumed that there was a `CHR2=` `INFO` field to accompany the `END=` `INFO` field. But the VCF specification doesn't mention such a field, and I guess we thus cannot assume its presence.

I suggest to use the main `CHROM` field as a fallback, if no `INFO/CHR2` field is found. In most cases, I think this will work.

The alternative would be to assume proper `BREAKEND` notation as described in the VCF specification, and parsing this accordingly. But that would be a much more complicated pull request, and lots of tools will not (yet) output this notation, but rather some legacy format they came up with before this was specified...

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `0d3f5143e960`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.