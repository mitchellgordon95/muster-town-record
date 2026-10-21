---
id: "dc_ypqynf36zy"
type: "report"
state: "building"
title: "No, Dara's secrets work is a design only: no code has shipped. Proposed split: host secrets never reach desks; collective secrets are managed at the Town Hall"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_ios62uyco3","dc_2t0d3fz8a1","dc_8hdfo4rucp"],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decisionNote: "you're a manager now, so i think you can delegate to her yourself."
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-21T20:54:41.779Z"
sessionId: "se_numsn6v7zv"
assignmentId: "as_zjck0hv2kh"
costUsd: 0.4934484
tokens: 344421
turns: 12
createdAt: "2026-10-21T20:52:16.702Z"
updatedAt: "2026-10-21T20:54:41.779Z"
---
## What I did
- Reread Dara's secrets design ([dc_ios62uyco3](../../article/2026-10/2026-10-21-design-secrets-for-muster-town-today-on-the-macboo-s62uyco3.md)) and checked main (16c9e4a) for any code from it.
- Wrote a note that sorts every secret into one of two tiers: [dc_8hdfo4rucp](../../note/2026-10/2026-10-21-secrets-which-belong-to-muster-town-the-host-and-w-dfo4rucp.md).

## Findings
- **Dara's secrets work is a design only.** No PR exists and nothing from it is in main.
  - Every `DESK_ENV_*` variable still reaches every desk (`session.ts:90`).
  - Desks still get your personal `gh` token by default.
  - Her PR 1 (per-building/skill grants, a limited env for host sessions, no admin token in logs) is waiting for you to say go.
- **The rule for the split: whose blast radius is it if it leaks?**
- **Muster Town (host) level.** The operator sets these over SSH in `/etc/muster-town/env`. They never show in the UI and never reach a desk:
  - GitHub sign-in client secret and the session secret
  - the admin token
  - the planned data-encryption key
  - the planned GitHub App private key
  - infrastructure keys: OVH, the deploy key and token, DNS
  - the server's own model login (your `CLAUDE_CODE_OAUTH_TOKEN`)
  - The Prod building's agents should reach infrastructure through narrow server verbs like `redeploy`, not raw keys.
- **Collective (Town Hall) level.** The collective's admin manages these in a Town Hall panel: values can be set but never read back, they're stored encrypted, and each is granted to a building, agent or skill:
  - donated Anthropic keys and subscription inputs. The Bank already does this; the keys still need encrypting at rest.
  - repo access for the collective's own repo
  - tool credentials for skills (e.g. `MINICLAW_WS_TOKEN` granted only to talk-to-wright)
  - API keys a building needs for its research
- **This changes Dara's design in one place.** She put the grants in `collective.json`, which only someone with repo access can edit. To be managed at the Town Hall, the grants and values move into the database behind an admin panel.
- **For the prod box, this changes one of my earlier asks.**
  - Set `CLAUDE_CODE_OAUTH_TOKEN` and a fine-grained PAT that covers only this repo, as before.
  - **Don't put the OVH keys in as `DESK_ENV_*`.** Until grants land, every desk would get a token that can delete the server.
  - Dara's PR 1 has to land before cutover.

## What I need from you
Decide whether this split is right; if it is, assign Dara PR 1 with the grants stored in the database and managed at the Town Hall, not in `collective.json`.

## Reply from Mitchell (2026-10-21 16:54)

you're a manager now, so i think you can delegate to her yourself.

