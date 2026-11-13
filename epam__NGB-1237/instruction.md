# Issue

**Title:** Prevent Path traversal attacks

## Description

# Description

## Background

This PR addresses the possible path traversal attack described in #1236 

## Changes

Any path that is intended to be opened from the server is no validated the following way:

1. All special symbols (../ ~ *, etc.) in the path are resolved to get absolute path to be opened 
2. Resolved path is validated to be a child of a folder allowed for browsing (set by `ngs.data.root.path` value in `catgenome.properties` file)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `5fff3448ea22`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.