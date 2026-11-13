# Issue

**Title:** Fix deprecation warnings

## Description

Hello! This fixes various deprecation warnings I ran into when going through the development guide. Most of them were in the python tests, which I've listed below for reference. More details about the fix for each are given in the commit messages.

```
tests/test_cli.py: 46 warnings
  /home/jacob/gsoc/msprime/msprime/cli.py:139: PendingDeprecationWarning: FileType is deprecated. Simply open files after parsing arguments.
    type=argparse.FileType("wb"),

tests/test_cli.py: 23 warnings
  /home/jacob/gsoc/msprime/msprime/cli.py:1147: PendingDeprecationWarning: FileType is deprecated. Simply open files after parsing arguments.
    type=argparse.FileType("rb"),

tests/test_cli.py::TestMspSimulateOutput::test_compress_warns
  /home/jacob/gsoc/msprime/msprime/cli.py:1301: UserWarning: The simulate command is deprecated but will continue to work indefinitely. To simulate ancestries, please use the 'ancestry' command. To place mutations on a tree sequence, please use the 'mutations' command.
    args.runner(args)

tests/test_mutations.py::TestMutationModelFactory::test_returns_mutation_model_instances_without_copying
tests/test_mutations.py::TestModelClasses::test_slim
  /home/jacob/gsoc/msprime/msprime/mutations.py:162: FutureWarning: SLiMMutationModel will be removed in future versions. Use SLiMv5MutationModel or SLiMv6MutationModel instead.
    warnings.warn(

tests/test_simulate_from.py::TestBasicFunctionality::test_from_wf_nonoverlapping
tests/test_simulate_from.py::TestBasicFunctionality::test_from_wf_overlapping
tests/test_simulate_from.py::TestSimAncestryInterface::test_extra_pops_missing_extra_metadata
tests/test_simulate_from.py::TestSlimOutput::test_minimal_example_no_recombination
tests/test_simulate_from.py::TestSlimOutput::test_minimal_example_recombination
tests/test_simulate_from.py::TestSlimOutput::test_single_locus_example_no_recombination
tests/test_simulate_from.py::TestSlimOutput::test_single_locus_example_recombination
tests/test_simulate_from.py::TestBugExamples::test_unordered_tables_on_output
  /home/jacob/gsoc/msprime/msprime/ancestry.py:1297: TimeUnitsMismatchWarning: The initial_state has time_units=unknown but time is measured in generations in msprime. This may lead to significant discrepancies between the timescales. If you wish to suppress this warning, you can use, e.g., warnings.simplefilter('ignore', msprime.TimeUnitsMismatchWarning)
    sim = _parse_sim_ancestry(

tests/test_ancestry.py::TestParseSimAncestry::test_sequence_length
  /home/jacob/gsoc/msprime/tests/test_ancestry.py:1172: TimeUnitsMismatchWarning: The initial_state has time_units=unknown but time is measured in generations in msprime. This may lead to significant discrepancies between the timescales. If you wish to suppress this warning, you can use, e.g., warnings.simplefilter('ignore', msprime.TimeUnitsMismatchWarning)
    sim = ancestry._parse_sim_ancestry(
```

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f5d1e339009c`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.