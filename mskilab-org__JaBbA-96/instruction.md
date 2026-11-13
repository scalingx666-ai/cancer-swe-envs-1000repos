# Issue

**Title:** Fixing a bug where the CPLEX check was forcefully implemented even when using Gurobi

## Description

**Description:**
- Addresses the issue where CPLEX check was ran even with Gurobi being used

**Changes:**
- added independent checks so that if gurobi is loaded, it will not run CPLEX check.
- if Cplex is present, but not gurobi, it will run CPLEX check for gGnome. If both gurobi and cplex is present, it will still run CPLEX check because by default JaBbA uses CPLEX unless otherwise mentioned gurobi.

**Impact:**
- Should address the issue where users were facing issues installing JaBbA when gurobi was being used as optimizer instead of CPLEX.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5dc966cdd7da`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.