# Issue

**Title:** Re-added sortbylength command (plus two seqdb sort changes)

## Description

Dear Dr. Edgar,

Thank you for open-sourcing usearch12 and for pointing to the old binaries. I needed the sortbylength command, so I re-implemented it in the v12 source based on the documented behavior on your website, and I am opening a pull request in case it is of any use to you or anyone else.

What I added:
- A new src/sortbylength.cpp implementing cmd_sortbylength().
- Wiring: o(sortbylength) in o_str.h, A(sortbylength) in cmds.h, and the object added to Makefile, Makefiled, and usearch12.vcxproj.

The command follows the documented options: -fastaout, -fastqout, -minseqlength, -maxseqlength, -topn, -relabel, and -sizeout. It sorts by decreasing length.

To make it work I also had to touch SeqDB::SortByLength() and SortBySize() in seqdb.cpp, and I wanted to flag two things there rather than hide them in the diff. I am not sure whether these are bugs or intended, so I am just describing what I saw:

1. SortByLength() has an early-out that checks whether the input is already sorted, but the PrevL comparison variable did not seem to get updated inside the loop (it stays UINT_MAX), so in my testing the check always concluded the data was sorted and the function returned without sorting anything. My first test run came back unsorted because of this. I added PrevL = L; inside the loop, which fixed it for me.

2. Both SortByLength() and SortBySize() reorder labels, lengths, and sequences but not m_Quals. As far as I can tell nothing in the current v12 source calls these functions, so this does not seem to affect anything today, but once a command actually sorts FASTQ data (as sortbylength -fastqout does) the quality strings ended up mismatched with the sequences. I added qual-pointer reordering (guarded by m_Quals != 0) to both, which resolved it. If you would rather keep that reordering inside the new command instead of in SeqDB, that is easy to change.

I have tested this on Linux, building with make CC=gcc CXX=g++. I have not tested on Mac or other systems. I tested FASTA and FASTQ input, the length filters, -topn, -relabel, and -sizeout, including a randomized check confirming strict descending order.

I need this for BPGA, and I saw some discussion where other people wanted it too, so I thought it was worth sharing. I understand further v12 development is unlikely, so please feel free to merge, adapt, or neglect any of this if it is of no use.

Thank you again for your work on usearch.

Note: it uses the usearch default minseqlength = 8, so seqs shorter than 8 are dropped unless -minseqlength is passed.

Best regards,
Anupam

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8797c9a80f4b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.