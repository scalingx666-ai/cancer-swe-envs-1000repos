# Issue

**Title:** Fix runtime failures with Numpy ≥ 2

## Description

This patch fixes the following symptom when running gubbins with Numpy version 2 and more:

	Running joint ancestral reconstruction with pyjar
	Traceback (most recent call last):
	  File "/usr/bin/run_gubbins", line 33, in <module>
	    sys.exit(load_entry_point('gubbins==3.4', 'console_scripts', 'run_gubbins.py')())
	             ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~^^
	  File "/usr/share/gubbins/gubbins/run_gubbins.py", line 166, in main
	    gubbins.common.parse_and_run(parser.parse_args(), parser.description)
	    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
	  File "/usr/share/gubbins/gubbins/common.py", line 373, in parse_and_run
	    jar(sequence_names = ordered_sequence_names, # complete polymorphism alignment
	    ~~~^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
	        base_patterns = base_pattern_bases_array, # array of unique base patterns in alignment
	        ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
	    ...<8 lines>...
	        verbose = input_args.verbose,
	        ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
	        max_pos = max_pos)
	        ^^^^^^^^^^^^^^^^^^
	  File "/usr/share/gubbins/gubbins/pyjar.py", line 646, in jar
	    node_pij = numpy.full((num_nodes,16), numpy.NINF, dtype=numpy.float32)
	                                          ^^^^^^^^^^
	  File "/usr/lib/python3/dist-packages/numpy/__init__.py", line 400, in __getattr__
	    raise AttributeError(
	    ...<3 lines>...
	    )
	AttributeError: `np.NINF` was removed in the NumPy 2.0 release. Use `-np.inf` instead.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f11e8404b263`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.