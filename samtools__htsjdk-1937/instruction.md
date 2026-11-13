# Issue

**Title:** Build the CSI index of an existing BGZF BCF through IndexFactory

## Description

`IndexFactory.createIndex(path, codec, IndexType.CSI, dictionary)` now builds the CSI index of an existing BGZF-compressed BCF, so a BCF written without `INDEX_ON_THE_FLY`, or by bcftools, can be indexed without bcftools.

- Before, a BCF had a CSI only if htsjdk wrote one on the fly. `IndexFactory`'s CSI path needs a text codec and failed with "Binary codecs does not support tabix" (found by GATK's IndexFeatureFile tests on 6.0).
- `IndexFactory` recognises a BCF by its contents, since callers may wrap the codec. `BCFFileReader.createCsiIndex()` reads the records into the index the writer builds on the fly. The new `BCFCsiIndex` writes it as the bare CSI `bcftools index` writes.
- `IndexType.TABIX` is refused for a BCF, as htslib refuses it. `IndexType.CSI` is refused for a BCF that is not BGZF-compressed. A file that can't be read still fails with a `TribbleException`, as before.
- The reader and the writer now start the index through one helper, `BCFCsiIndex.binningIndexBuilderFor(VCFHeader)`. This fixes two bugs in on-the-fly indexing, which is new in 6.0. Both failed before; both now match bcftools:
  - A header whose contig lines give no `length=` got an index reaching only 131,072 bases. It now reaches 2^31 - 1, as htslib does.
  - A record at POS 0 (a telomere) is indexed at 1, as htslib indexes it.
- `getFeatureReader(resource, codec, Index)` now refuses a TBI or CSI index given in memory (`TabixIndex` or `BCFCsiIndex`). It always builds a `TribbleIndexedFeatureReader`, which reads their BGZF virtual offsets as file offsets. A BCF query then found nothing, and a bgzipped VCF query through an in-memory TBI failed with a parse error on compressed bytes. The message points to the overloads that take an index path, which pick the right reader. Nothing in GATK, Picard or IGV uses this overload.
- Error messages that told users to run `bcftools index` now also name `IndexFactory`. `IndexFactory.loadIndex` on a bare CSI says that such an index is read through the file it indexes.
- Checked against `bcftools index --csi` (1.24): the indexes are equal (`BinningIndex.equals`). Inputs: htsjdk-written BCFs with block-aligned records, long END/SVLEN records, empty and sparse contigs, 200 KB records, contigs without lengths, POS 0, and bcftools' own `vqsr.bcf` (131,821 records, 0.9 s). Tests compare with bcftools when it is installed.
- Known gaps:
  - Records must follow the header's contig order. htslib takes contigs in any order, as long as each contig's records are together. Allowing that would change `BinningIndex.Builder`, which BAM, CRAM and tabix share.
  - When the highest-numbered contigs of a sparse-IDX header have no records, `n_ref` differs from bcftools'. Queries are unaffected.
- CHANGELOG: new VCF bullet.

Reviewed with Sonnet and Opus.

<!-- This is an auto-generated comment: release notes by coderabbit.ai -->

<!-- coderabbit-ai-generated:v1 -->

## Summary by CodeRabbit

* **New Features**
  * Added CSI indexing support for existing BGZF-compressed BCF files, including index creation and region-based queries.
  * CSI indexes can also be generated while writing BCF files, including for records at position zero and contigs without declared lengths.
* **Bug Fixes**
  * Improved error messages for unsupported index and input combinations, and clarified that CSI indexes without tabix headers must be read alongside their indexed files.

<!-- end of auto-generated comment: release notes by coderabbit.ai -->

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `39fac6ae3995`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.