# Issue

**Title:** Add Azure AI Foundry support for academic institutions

## Description

## Summary

Enables celltype-cli to authenticate via Azure AI Foundry, so researchers at academic medical centers and universities that provision Claude through Azure can use `ct` with their existing Foundry credentials.

- Detect `ANTHROPIC_FOUNDRY_API_KEY` and `ANTHROPIC_FOUNDRY_RESOURCE` as valid auth
- Use `AnthropicFoundry` client for direct LLM calls
- Set `CLAUDE_CODE_USE_FOUNDRY=1` for Agent SDK subprocess routing
- Skip `sk-ant-` key prompt in `ct setup` when Foundry is configured
- Show "Azure Foundry" in `ct doctor` output
- Mention Foundry as an option in the "API key not configured" error message
- Bump `anthropic>=0.74.0` (minimum for `AnthropicFoundry` class)
- Add Foundry-specific unit tests

**7 files changed, 69 insertions, 11 deletions.**

## Verified end-to-end

Tested with real Azure AI Foundry credentials at an academic institution. Full agentic loop works: tool search, protein function prediction, disease association queries, expression profiling, and synthesis.

<img width="798" height="486" alt="Screenshot 2026-02-24 at 16 29 24" src="https://github.com/user-attachments/assets/2555fb7f-2da7-4988-8b94-1f76b08ed4e4" />

### ct doctor
```
llm  │ ok  │ provider=anthropic (Azure Foundry), model=claude-sonnet-4-6
```

### ct setup
```
Azure AI Foundry detected. No API key needed.
```

### Usage
```bash
export ANTHROPIC_FOUNDRY_API_KEY="your-key"
export ANTHROPIC_FOUNDRY_RESOURCE="your-resource"
ct config set llm.model claude-sonnet-4-6
ct "What is BRCA1?"
```

## Test plan

- [x] `ct doctor` shows "Azure Foundry" when Foundry env vars are set
- [x] `ct setup` detects Foundry and skips key prompt
- [x] `ct "What is BRCA1?"` runs full agentic loop through Foundry
- [x] Standard `ANTHROPIC_API_KEY` users see zero behavior change
- [x] 34/34 unit tests pass
- [x] Error message mentions Foundry when no auth is configured

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `21b91bc727a6`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.