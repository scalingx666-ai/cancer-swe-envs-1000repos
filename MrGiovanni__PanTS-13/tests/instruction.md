# Issue

**Title:** Show DH Third Place certificate as image in README

## Description

The certificate PDF was linked as a badge; the goal is to render it visually inline in the README.

## Changes
- Converted `document/DH_Third_Place_PanTS_Health_Certificate.pdf` → `document/DH_Third_Place_PanTS_Health_Certificate.png` (150 DPI via `pdftoppm`)
- Replaced the badge link in the Paper section with the PNG rendered inline at 600px width, clicking through to the original PDF

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `9119b8d19723`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.