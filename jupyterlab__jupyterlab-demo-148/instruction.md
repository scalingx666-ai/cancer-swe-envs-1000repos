# Issue

**Title:** Simplify CI, fix mybinder.org build, bump python (and other) versions

## Description

I started looking into this more as it was reported broken on mybinder.org: https://jupyter.zulipchat.com/#narrow/channel/469744-jupyterhub/topic/try.20mybinder.20jupyterleab.20demo.20broken

Debugging the failure on mybinder.org via  I discovered:

1. xeus-cling+friends was causing mamba to fail to solve
2. mybinder.org's build memory limits were causing mamba to fail
3. CI was failing here for unrelated reasons

(2) is fixed with  and this 'fixes' (1) by removing xeus-cling. I also unpinned the semi-pinned versions in `environment.yml`. If we want version pinning, we should use a lock file. This bumps up versions of various packages, including python (to 3.12 from 3.9)

This works on mybinder now! https://mybinder.org/v2/gh/yuvipanda/jupyterlab-demo/remove-xtensor?urlpath=lab

Merging this will unbreak this repo on mybinder.

I then looked through CI, and simplified it by:

1. Not taking on the responsibility of setting up environments in our build script. This fundamentally was the major reason for complication, as first CI setup an environment and then the environment tried to do more complex things with environments. Now environment is only set up on CI, and on local machines, it's the user's responsibility to setup environment. 
2. Getting rid of `pyinvoke` and turning things into a simple `build.py` file. `invoke` is great for things that are more complex with multiple interdependencies. By removing environment management, what needs to happen got far more simpler - clone some repos, and copy some files. This can be done with straightforward python more easily, which I have done here.
3. Only port the demofiles and talks invoke targets, and ignore everything else. This means the one for updating environments is also removed - as that should instead be done via lockfiles.
4. Add irkernel back to the environment.yml file, as that was required for CI to pass. This does bring back rstudio into the mybinder launch, but that's fine.

Originally reported in https://jupyter.zulipchat.com/#narrow/channel/469744-jupyterhub/topic/try.20mybinder.20jupyterleab.20demo.20broken

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `24a396b12aa0`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.