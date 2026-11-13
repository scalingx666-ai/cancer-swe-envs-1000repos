# Issue

**Title:** Fix for get.cormat when VST is not feasible

## Description

Hi Tinyi,

I've run into an infrequent problem with some use cases, but also think I figured out a fix. When I run run.Ted() with input.type = "scRNA" and tum.key, cell.type.labels, and cell.subtype.labels all specified, everything works as expected when there is at least one gene with no zeros in the estimated tumor expression profile. However, sometimes the tumor expression profile has at least one zero for all genes, and then after the final sampling I get the following message when considering VST (as expected):

> [1] "every gene has at least one zero. vst transformation is NOT feasible"

However immediately after this message, the program fails with the following error message:

> Error in get.cormat(Zkg.tum = Zkg.tum.norm) : 
>   object 'Zkg.tum.norm' not found

And no output comes out of the run.Ted function. I believe this is because the full location of Zkg.tum.norm (e.g. ted.res$res$first.gibbs.res$Zkg.tum.norm) is not defined in this vst code block, as it is for Zkg.tum above in this block. I believe this commit fixes this. 

I tried to verify this on my data by re-running the same run.Ted() call with this change to the code, but it actually said VST was feasible this time. Perhaps this is due to some random element of the sampling, as I think I used the same call/reference.

Best,
Tom

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `21d39c1281e4`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.