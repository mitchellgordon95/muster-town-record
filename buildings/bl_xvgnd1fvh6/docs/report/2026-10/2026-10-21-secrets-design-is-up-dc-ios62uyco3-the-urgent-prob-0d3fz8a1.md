---
id: "dc_2t0d3fz8a1"
type: "report"
state: "building"
title: "Secrets design is up (dc_ios62uyco3). The urgent problem: every coding desk gets Mitchell's personal GitHub token"
authorId: "ag_8uq6fnjis4"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-21T19:51:14.265Z"
sessionId: "se_da1wm7wgmh"
assignmentId: "as_0di1sjm26g"
costUsd: 0.8659695000000001
tokens: 26231
turns: 21
createdAt: "2026-10-21T18:56:46.140Z"
updatedAt: "2026-10-21T19:51:14.265Z"
---
## What I did
I traced every path a secret takes in the code (main b956616), checked from inside my own desk what actually arrives there (key names and token scopes only, never values), and wrote the design: [Design: secrets for Muster Town](../../article/2026-10/2026-10-21-design-secrets-for-muster-town-today-on-the-macboo-s62uyco3.md). I sent Cleo the parts that affect her VPS setup. I changed no code and opened no PR.

## Findings
- **Worst problem: every coding desk gets Mitchell's personal GitHub token.** The default setting `desks.ghToken: "gh-cli"` passes the host's `gh auth token` to every desk in a building with code access. From my desk it shows as a `gho_` token with scopes `repo, admin:public_key, gist, read:org`: write access to all his repos, plus the ability to add SSH keys to his account. Code: `runtime/src/desk/session.ts:96`.
- **Every `DESK_ENV_*` variable reaches every desk in every building** (`session.ts:88`). From my desk I can see the OVH keys and `MINICLAW_WS_TOKEN`. The subscription token and fallback API key also go into every desk.
- **The database holds usable credentials:**
  - Agent, user and admin tokens are stored in plaintext and never expire. Each agent has one token for life.
  - Donor API keys are stored in plaintext.
  - Planned Litestream backups would copy all of this to R2.
- **Admin token in logs:** it's printed to stdout on every start (`server/src/main.ts:47`).
- **Host sessions inherit the full server environment** (`runtime/src/sdk.ts:121`).
- **Design, in short:**
  1. Grants per building, agent or skill, listed by name in `collective.json`. Desks get nothing that isn't granted.
  2. A GitHub App that mints a token per session, limited to the town repo and valid for 1 hour.
  3. Town tokens issued per session and stored hashed; donor keys encrypted.
  4. On the VPS: systemd encrypted credentials at runtime (not in the environment, so child processes don't inherit them), with sops+age in a private repo as the source of truth. OVH Barbican and Vault aren't worth it yet.
  5. Later, a model proxy so desks never hold the Anthropic key. Unverified: whether this works for subscription tokens.
  6. When we move to the VPS, rotate every secret that has ever been in a desk.
- **Proposed next session:** PR 1. It adds the scoped grants, gives host sessions a limited set of environment variables, and stops printing the admin token.

## What I need from you
Replace the gh-cli token now: make a fine-grained GitHub token (agent-town repo only; contents and pull requests read/write), put it in `.env` as `GH_TOKEN`, and set `desks.ghToken` to `"env"`. Also tell me whether to start PR 1.
