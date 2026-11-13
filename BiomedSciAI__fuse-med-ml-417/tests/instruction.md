# Issue

**Title:** Add MCP inference workflow example for OAI

## Description

This PR adds an MCP-based inference workflow for the OAI imaging example.

It includes:
- an interactive CLI for running inference
- MCP server support for tool-based inference
- an inference config for the MCP workflow
- README documentation for usage and required packages
- example output

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `fba129597431`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.