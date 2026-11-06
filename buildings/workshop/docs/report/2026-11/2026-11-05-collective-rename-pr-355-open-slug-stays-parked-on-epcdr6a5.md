---
id: "dc_j4epcdr6a5"
type: "report"
state: "building"
title: "Collective rename: PR #355 open (slug stays); parked on CI"
authorId: "ag_3ezjrsy1iq"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved: PR #355 renames a hosted collective (hub row + collective.json + mounted town.name) with the slug untouched; Planning desk → System → This collective → Rename for admins; root-admin PATCH /api/collectives/:slug. Your parked continuation handles CI → merge → report the merge sha (no redeploy). Mitchell renames Trauma himself once live; that goes in rollup 49's \"What you'd see\"."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-05T19:02:51.328Z"
sessionId: "se_lez5je6qcs"
assignmentId: "as_bxid6jy3hd"
costUsd: 1.2952434000000002
tokens: 64762
turns: 26
createdAt: "2026-11-05T19:02:42.839Z"
updatedAt: "2026-11-05T19:02:51.328Z"
---
## What I did
Built a rename for hosted collectives that leaves the slug alone, for Mitchell's flag [dc_hz1nz88pkt](../../flag/2026-11/2026-11-05-i-d-like-to-be-able-to-rename-my-collective-1nz88pkt.md). Opened draft PR https://github.com/mitchellgordon95/muster-town/pull/355 and parked it on CI.

## Findings
- The slug and the name were already separate. The slug is the hub.db primary key and the address; the name is its own column. But `seedDefaults` rewrites the town name from collective.json **on every boot** (core/src/seed.ts:148). So a rename has to update the file too, or it reverts at the next restart.
- `Hub.rename(slug, {name})` (server/src/hub.ts) updates three things together, and the slug is never touched:
  - the hub row (homepage tile),
  - collective.json (other keys kept),
  - the mounted World's `town.name` (HUD).
  
  It refuses a retired collective, and the name must be 1–80 characters.
- Routes:
  - `PATCH /<slug>/api/collective {name}`: for the collective's own admins, same gate as retire.
  - `PATCH /api/collectives/:slug {name}`: for root (Workshop) admins.
- UI: Planning desk → System → "This collective" has a Name field and a Rename button, admins only. The hint reads "The address muster.town/<slug> stays."
- Tests: added one case to server/test/hub-start.test.ts covering:
  - refused for a non-admin (403), when signed out (401), for a blank name (400), and for an unknown slug (404);
  - the hub row, collective.json, `/api/town` name and `/api/collectives` all change, and the slug stays;
  - a root admin can rename; another collective's owner can't.
  
  hub-start passes 11/11 and typecheck is green. The full local run reported 35 files / 293 tests passed.
- **Next session (on CI):** if CI is green, mark the PR ready, merge it and report the merge commit (no `redeploy`). If red, fix it. Then, once it's live, Mitchell renames Trauma at **muster.town/trauma/ → Town Hall → Planning desk → System tab → This collective → Name "Trauma Town" → Rename**. As root admin he could also send `PATCH /api/collectives/trauma`. An agent has no human cookie, so it can't do this for him.

## What I need from you
Nothing needed.
