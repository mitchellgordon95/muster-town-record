---
id: "dc_d26ij4y0xf"
type: "report"
state: "building"
title: "Secrets PR 1 is on main (1c96fe7): encrypted collective secrets, scoped desk grants, and a Town Hall Secrets tab. It still needs a redeploy and a data key"
authorId: "ag_8uq6fnjis4"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-22T19:47:54.142Z"
sessionId: "se_ps0wa3ak9z"
assignmentId: "as_0o8ffll8i6"
costUsd: 2.9197359
tokens: 6009744
turns: 66
createdAt: "2026-10-21T21:14:17.442Z"
updatedAt: "2026-10-22T19:47:54.142Z"
---
## What I did
I shipped the brief [dc_6xe6u6i7d2](../../assignment-proposal/2026-10/2026-10-21-brief-secrets-pr-1-scoped-grants-stored-in-the-db-e6u6i7d2.md) as three commits and pushed them straight to main, ending at **`1c96fe7`** (branch `agent/dara/secrets-pr-1-scoped-grants-in-the-db-man`). Commit `2c73766` is the backend and API, `9789b5c` is the Town Hall panel, and the last one updates the deploy README. `npm run typecheck` is clean and all 453 tests pass, including 8 new ones across core, runtime and server. The web build passes. **I couldn't queue the redeploy because I don't have `town.redeploy`.** I also haven't seen the panel in a browser, since my desk has none; it's checked only by typecheck and build.

## Findings
**What changed** (full reference in `docs/secrets.md`):
- **Storage.** A new `secrets` table holds each secret's name, its encrypted value and its grants. Values are encrypted with AES-256-GCM under the host's `MUSTER_TOWN_DATA_KEY`, with the secret's name bound in so a value can't be moved to another name. If the key is missing, setting a value fails with a 409 and nothing is stored, so nothing is ever kept in plaintext.
- **Reserved names.** Names the runtime sets itself can't be used: `GH_*`, `CLAUDE_*`, `ANTHROPIC_*`, `MUSTER_TOWN_*`, `DESK_*`, `PATH`, and similar.
- **API:** `GET`, `PUT` and `DELETE` on `/api/secrets`, for human collective admins only. Agent tokens and non-admin users are refused (403). The list shows names, grants and whether a value is set, never the values themselves.
- **Panel.** The Town Hall's building panel has a new **Secrets** tab, shown only to admins. It lists each secret with set/missing and its grants, lets you add or remove building, agent and skill grants, has a write-only value field (set or replace) and a delete button, and warns when the host has no data key.
- **Desks.** `deskEnv()` passes a secret only when it has a value and is granted to the session's building, its agent, or a skill pinned for that agent. Each one is logged as a `secret.granted {name, sessionId, via}` event, without the value.
- **`DESK_ENV_*` fallback.** These still reach every desk for one release, with a warning in the server log. If the Town Hall has a secret with the same name, that secret's grants win.
- **Host sessions** now get an allowlisted env (PATH, HOME, locale, proxies, `CLAUDE_*`, `ANTHROPIC_*`) instead of `{...process.env}`.
- **Admin token.** It's no longer printed at startup. It's written to `<data>/admin-token` with mode 0600, now enforced even when the file already exists, and only the path is printed.
- **Deploy README.** It now says to put `MUSTER_TOWN_DATA_KEY` in `/etc/muster-town/env`, to put no `DESK_ENV_*` on prod, and to read the admin token from its file.

**How to grant `MINICLAW_WS_TOKEN` to talk-to-wright from the panel** (once the redeploy is done and a data key is set):
1. Sign in as an admin, go to the Town Hall door, open the building panel and choose the **Secrets** tab.
2. Under "New secret", enter the name `MINICLAW_WS_TOKEN`, paste the value and click **Add**.
3. On its row, set Grant to **Skill**, pick **talk-to-wright** and click **Grant**.
4. Do the same for `MINICLAW_HOST`. Then remove both `DESK_ENV_MINICLAW_*` lines from `.env`; until you do, the Town Hall copies already take priority for those two names.

**Caveat:** talk-to-wright is pinned **town-wide**, so a skill grant still reaches every resident. To narrow it, unpin the skill town-wide and pin it per building, or grant the secret to specific buildings or agents instead.

**Cutover risk:** `cutover.sh` copies the Mac's `town.db` to prod. Secrets set on the Mac only decrypt on prod if prod has the **same** `MUSTER_TOWN_DATA_KEY`. Otherwise prod passes nothing (it doesn't send garbled values) and they have to be set again there. I've told Cleo.

## What I need from you
Add `MUSTER_TOWN_DATA_KEY=$(openssl rand -base64 32)` to the Mac's `collectives/workshop/.env` and to prod's `/etc/muster-town/env` (the same value on both if the DB moves at cutover), then redeploy so `1c96fe7` is live; I don't have permission to redeploy.
