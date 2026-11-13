# Issue

**Title:** Optimize file operations in download scripts: 40x performance improvement

## Description

The download scripts used `seq`-based loops spawning 9,901 individual `mv` processes. This is inefficient and slow.

## Changes

### File moving optimization (`download_PanTS_label.sh`)
Replaced sequential subprocess calls with batched `find + xargs` operations:

**Before:**
```bash
for i in $(seq 1 9000); do
    folder=$(printf "PanTS_%08d" "$i")
    mv "LabelAll/$folder" LabelTr/
done
# 9,901 subprocess calls, ~18s
```

**After:**
```bash
find . -maxdepth 1 -type d \( \
     -name 'PanTS_0000[0-8]*' -o \
     -name 'PanTS_00009000' \
\) -print0 | xargs -0 -r mv -t ../LabelTr/
# 2 operations, ~0.45s, 40x faster
```

### Progress indicators (both scripts)
Added `--checkpoint` flags to tar operations for user feedback during multi-GB extractions:

```bash
tar -xzf "$file" -C ImageTr --checkpoint=500 --checkpoint-action=echo="."
```

### Pattern matching
- Uses tight glob `PanTS_0000[0-8]*` to match files 1-8999
- Explicitly includes `PanTS_00009000` for training set
- Remaining `PanTS_00009*` files (9001-9901) route to testing set
- Safe filename handling with `-print0` / `xargs -0`

<!-- START COPILOT CODING AGENT SUFFIX -->

<details>

<summary>Original prompt</summary>

> Identify and suggest improvements to inefficient code

</details>

<!-- START COPILOT CODING AGENT TIPS -->
---

💡 You can make Copilot smarter by setting up custom instructions, customizing its development environment and configuring Model Context Protocol (MCP) servers. Learn more [Copilot coding agent tips](https://gh.io/copilot-coding-agent-tips) in the docs.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `a9f6e3fa5044`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.