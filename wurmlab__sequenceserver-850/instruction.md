# Issue

**Title:** Align gem versions with the other sequenceserver-cloud apps

## Description

The sequenceserver-cloud Docker image installs the gems of every app from its own Gemfile.lock. When two lockfiles lock different versions of one gem, the image gets both versions. This change locks the same versions as the other apps: for each gem, the highest version that one of them already uses.

## Changes

- Bundler 2.5.17 → 4.0.23 (BUNDLED WITH)
- rack 3.2.6 → 3.2.7

## Verification

CI on this PR runs the specs with Ruby 3.3 and Bundler 4.0.23. selenium-webdriver stays different in sequenceserver (`~> 4.35.0` in the gemspec). It is a test gem, so the Docker image does not install it.

🤖 Generated with [Claude Code](https://claude.com/claude-code)

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a16725c82c3a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.