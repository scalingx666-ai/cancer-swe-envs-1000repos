# Issue

**Title:** add requirements to setup.py

## Description

Hello,

First of all: thanks for making this awesome software!

Currently, peddy happily installs from pypi. However, since run requirements are not listed in the setup.py, those won't get auto-installed by pip. This means the users to has to manually install the dependencies if they use PyPi. 

This PR adds the requirements to the setup.py. I've also taken the liberty to modify the travis.yml so that, instead of doing `pip install requirements.txt && python setup.py install`, it runs `pip install '.'`. The latter somewhat emulates the behavior of a regular pip install, and auto-installs dependencies.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `f8158124273e`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.