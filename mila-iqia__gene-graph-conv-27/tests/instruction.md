# Issue

**Title:** Create datastore path

## Description

I made these changes a while back to get the graphs to load using any datastore location. It should default to the local "./data" folder like it is now.

I tested it as follows:

graph = data.gene_graphs.HetIOGraph(datastore="/network/data1/genomics/graphs")
graph = data.gene_graphs.GeneManiaGraph(datastore="/network/data1/genomics/graphs")
graph = data.gene_graphs.HumanNetV2Graph(datastore="/network/data1/genomics/graphs")
graph = data.gene_graphs.HetIOGraph(datastore="/network/data1/genomics/graphs")
graph = data.gene_graphs.StringDBGraph(datastore="/network/data1/genomics/graphs")

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8d749e111c87`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.