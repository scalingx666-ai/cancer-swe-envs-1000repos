# Issue

**Title:** bugfixes: build and calc_inp_dims_given_outp_after_upsample

## Description

In build():
 - when calling block.build, there was an error when conv_pad_mode_per_layer had length zero. This can be recreating by running the tinyCnn example, which has len(conv_pad_mode_per_layer) for the FC layers. If this is the case, now the default None is passed.

In calc_inp_dims_given_outp_after_upsample():
- outp_dims_in_hr[d] has type 'Dimension' and the operator / cannot process 'Dimension' and 'int'. Casting outp_dims_in_hr[d] to int fixes the issue

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `66cf2cc64e0a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.