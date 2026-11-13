# Issue

**Title:** Add GitHub Actions workflow for multi-platform builds including macOS

## Description

- [x] Create `.github/workflows` directory structure
- [x] Create GitHub Actions workflow file for multi-platform builds
- [x] Configure workflow to build for common targets:
  - [x] Linux x86_64
  - [x] Linux i386
  - [x] macOS x86_64 (Intel)
  - [x] macOS arm64 (Apple Silicon) - included instead of i386 since Apple dropped 32-bit support
  - [x] Windows x86_64
- [x] Set up Nim compiler installation in workflow
- [x] Configure build steps for each platform
- [x] Set up artifact uploading for built binaries
- [x] Configure release publishing on version tags
- [x] Verify workflow syntax and configuration
- [x] Create BUILD.md with detailed build instructions
- [x] Update README.md with information about multiple platform support
- [x] Update runner versions to latest (ubuntu-22.04, macos-13, windows-2022)
- [x] Update artifact actions to v4 to fix deprecation warnings
- [x] Fix build issues: add bin entry to nimble file and remove invalid --verbose flags
- [x] Fix i386 Linux build package conflicts

## Summary

Created a comprehensive GitHub Actions workflow that builds jigv for multiple platforms:
- **Linux**: x86_64 and i386 (32-bit) on Ubuntu 22.04
- **macOS**: x86_64 (Intel) and ARM64 (Apple Silicon) on macOS 13
- **Windows**: x86_64 on Windows Server 2022

### Key Features:
1. Automatic builds on push, PR, and tags
2. Cross-platform support with proper dependency installation
3. Artifact uploads for each platform
4. Automatic release creation when version tags are pushed
5. Caching of Nim dependencies for faster builds

### Latest Updates:
- Updated all runner versions to avoid deprecated images (Ubuntu 22.04, macOS 13, Windows Server 2022)
- Updated `actions/upload-artifact` and `actions/download-artifact` from v3 to v4 to resolve deprecation warnings
- Added `bin = @["jigv"]` to jigv.nimble to fix nimble build command
- Removed invalid `--verbose` flag from nim compile commands
- Fixed i386 Linux build by skipping amd64 dependency installation to avoid package conflicts

### Note on i386 macOS:
32-bit macOS builds are not included because Apple discontinued 32-bit app support in macOS 10.15 Catalina (2019), and modern Nim and dependencies don't support it. However, ARM64 (Apple Silicon) support is included, covering all modern Mac users.

<!-- START COPILOT CODING AGENT SUFFIX -->

<details>

<summary>Original prompt</summary>

>
> ----
>
> *This section details on the original issue you should resolve*
>
> <issue_title>macOS build</issue_title>
> <issue_description>Any chance you have a build for i386 macOS?   Or lacking that, instructions?  Do you know if its successfully been done?
>
> Thanks
>
> </issue_description>
>
> <agent_instructions>create a github action to build for common targets including i386 osx
> </agent_instructions>
>
> ## Comments on the Issue (you are @copilot in this section)
>
> <comments>
> </comments>
>

</details>

Fixes brentp/jigv#25

<!-- START COPILOT CODING AGENT TIPS -->
---

💬 Share your feedback on Copilot coding agent for the chance to win a $200 gift card! Click [here](https://survey3.medallia.com/?EAHeSx-AP01bZqG0Ld9QLQ) to start the survey.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `dfcb37e16d1a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.