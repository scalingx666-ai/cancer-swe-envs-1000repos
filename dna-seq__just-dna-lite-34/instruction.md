# Issue

**Title:** Explain when a catalog account is needed and how to create one

## Description

## Summary
You only need a catalog account if you want to publish a module, claim a namespace, or ask the server to validate a module before publishing. Browsing the catalog, downloading modules, and annotating a genome do not need one. Building a module and running it on your own genome does not need one either.

There is no email and no password. The account is created by your computer. You get an API token, which the program sends when you publish, and an install-id, which is the only way to get a new token for the same account if you lose the first one. Nobody can reset it for you.

The new guide, docs/REGISTRY_ACCOUNT_SETUP.md, walks through both ways to create the account:

- In the app: Module Catalog, pick the server, type a display name, create a namespace. The token shows up in the Account pane.
- From the command line: `pipelines registry register`, save the token in the root `.env`, then claim the namespace.

It also says where `.env` goes (the just-dna-lite folder you run `uv run start` from, not `webui/`), that the test server and the public catalog are two separate accounts, and that a claim on the public catalog cannot be undone. PUBLISHING.md now points at this guide first. `.env.template` names the two token variables and says they are only for publishing.

## Test plan
- [ ] Read docs/REGISTRY_ACCOUNT_SETUP.md and confirm the table of who needs an account matches what the app allows without a token
- [ ] Confirm docs/PUBLISHING.md opens with the link to the new guide
- [ ] Confirm .env.template lists REGISTRY_TOKEN and REGISTRY_TOKEN_POLYGON as comments, with no real token

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `8bc9528312df`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.