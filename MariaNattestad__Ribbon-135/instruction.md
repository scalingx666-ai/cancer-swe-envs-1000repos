# Issue

**Title:** fix: paired-end BAM coloring bug + signed BAI URL support

## Description

Color reads by: Which BAM file each read came from" always rendered every read the same color when viewing paired-end data. parse_paired_end() merges a read's two mates into one chunk and set raw.bam from the merged {first, second} wrapper object, which never had a .bam field itself - the index set in my_fetch() lives one level deeper, on record.first.raw.bam. Fixed by reading it from there.

Also added an optional "bam_url|bai_url" pairing in read_bam_urls(), for BAMs served via time-limited signed URLs (e.g. GCS/S3 presigned GET URLs). BamFile.mount() derives the BAI URL by appending ".bai" to the BAM URL, which breaks a signed URL's query-string signature and doesn't point at a validly-signed BAI object anyway - the BAI needs its own independent signature. Passing both explicitly as "bam_url|bai_url" (falling back to the existing ".bai"-suffix behavior when no "|" is present) works around this without changing the default single-URL case.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `c9fc688418db`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.