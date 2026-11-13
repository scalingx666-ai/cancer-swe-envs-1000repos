# Issue

**Title:** Fix: Remove PapersWithCode API & Backfill papers since 2025-07-17

## Description

## 📝 Description
The daily automated update workflow has been failing recently due to the **PapersWithCode API** (`arxiv.paperswithcode.com`) being down or unstable. This caused SSL handshake errors that blocked new papers from being saved.

## 🛠️ Changes
1. **Removed PapersWithCode API Dependency:**
   - Modified `daily_arxiv.py` to stop fetching code links from `arxiv.paperswithcode.com`.
   - This prevents the script from crashing/skipping papers due to API connection errors.

2. **Data Update:**
   - Backfilled missing papers for all categories from **2025-07-17** to the present.

## Related Issue
Vincentqyw/cv-arxiv-daily#16

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `22cfa4ca2d53`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.