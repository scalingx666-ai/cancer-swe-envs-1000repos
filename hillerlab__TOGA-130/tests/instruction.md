# Issue

**Title:** Fix nucleotide.fasta alignments

## Description

--- feedback welcome! :)

**Major changes:**
- nucleotide.fasta now outputs the CESAR2.0 exon alignments

**Minor changes:**
- Added an option to stop the pipeline at any step, when using toga.py interactively (rather than from the command line; this is useful mostly for debugging and development)
- Added some unit tests using the built-in doctest module
- Added some type hints
- Removed some unused function parameters

**How to test these changes:**
Run the doctest module like so:

```
$ python3 -m doctest -v modules/merge_cesar_output.py
```

The expected output is:

```
Trying:
    from pprint import pprint
Expecting nothing
ok
[...]
7 items had no tests:
    merge_cesar_output
    merge_cesar_output.get_excluded_genes
    merge_cesar_output.main
    merge_cesar_output.merge_cesar_output
    merge_cesar_output.parse_args
    merge_cesar_output.split_ex_reg_in_chrom
    merge_cesar_output.split_ex_reg_in_chrom__direction
3 items passed all tests:
   4 tests in merge_cesar_output.parse_cesar_out_file
   1 tests in merge_cesar_output.read_fasta
   1 tests in merge_cesar_output.read_region
6 tests in 10 items.
6 passed and 0 failed.
Test passed.
```

**Why doctest for a testing framework**

I wanted something that would not add complexity to the source code. To this end, doctest is probably the best option: it's a built-in standard library, the unit tests are written into function docstrings, and the test syntax is basically the same as copy-pasting from an interactive python session.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `ac0578ecaa09`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.