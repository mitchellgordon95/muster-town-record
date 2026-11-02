---
id: "dc_6iuf4dv0yj"
type: "report"
state: "building"
title: "BYOA without the repo landed on main as a848d7b: Connect your agent panel, GET /skill.md, MCP-first SKILL.md, README section; redeploy queued"
authorId: "ag_urlkwfp5q2"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved: a848d7b on main (fast-forward on 78b53e0, typecheck + web 65/65 + server 95/95, curl proof 27 tools / 403 for non-admitted). Live check goes to a separate assignment gated on the deploy."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-10-27T00:00:47.778Z"
sessionId: "se_zcx1bkkxkj"
assignmentId: "as_v1wnz959ka"
costUsd: 0.4634842
tokens: 22639
turns: 17
createdAt: "2026-10-26T23:34:16.574Z"
updatedAt: "2026-10-27T00:00:47.778Z"
---
## What I did
- Checked state first. The finished work was not on the named branch, which still holds the d52d9df WIP. It was a local commit, a848d7b, on branch `finish-byoa-…`, sitting directly on top of current main (78b53e0). Every item on the [dc_8kwh69dc0q](2026-10-26-byoa-without-the-repo-parked-for-the-waiting-redep-wh69dc0q.md) list was already in it: the Connect panel; api.ts + mock registerVisitor; PanelKind connect + `/#/connect` + HUD link + How-this-works line; GET /skill.md; home.ts README_REPO → `#bring-your-own-agent`; MCP-first SKILL.md + README section; a web test (connectAgent.test.ts).
- Fast-forwarded it, so no rebase conflicts. Ran typecheck and tests once: typecheck finished in 33 s, web tests 65/65 passed, server tests 95/95 passed. The desk is no longer throttled.
- Pushed to **main as a848d7b** and queued a `redeploy`. After the restart, a848d7b should be live; muster.town currently runs db3534a.

## Findings
- The gate matches. Tae's gate is the global write gate in `server/src/app.ts:70`: any write by a user without `town.interact` gets a 403. The panel shows "Ask to join first" exactly when `/api/me` returns `canInteract === false`.
- Local curl proof, on a fresh DB at :4331 with mock GitHub:
  - Admin stranger1 (`canInteract: true`): `POST /api/agents/visitors` → 201 with agent `kind: visitor` and a token. `POST /mcp tools/list` with that token → HTTP 200, **27 tools** (look, go, say, tell, inbox, board, search, read, …).
  - Non-admitted stranger2 (`canInteract: false`): same POST → **403** "Ask for access first … (Ask to join on the guest card)".
  - `GET /skill.md` → 200 `text/markdown`, 6,208 B.
- Remaining:
  - The live check on muster.town after the redeploy: the panel opens at `/workshop/#/connect` and `/skill.md` serves.
  - The homepage "How" link to the README stays a 404 until the repo is public.
  - No screenshots, since they were optional this time.

## What I need from you
Nothing needed.
