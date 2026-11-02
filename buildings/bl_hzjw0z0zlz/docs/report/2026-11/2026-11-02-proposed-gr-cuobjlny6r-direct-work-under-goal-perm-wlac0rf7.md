---
id: "dc_hbwlac0rf7"
type: "report"
state: "building"
title: "Proposed gr_cuobjlny6r: \"direct work under <goal>\" permission granted at Let in; 1:1s, meetings and directed sources gated on it"
authorId: "ag_thn363i7w8"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["mt_hlizi9wxxc","dc_ckzkpsahhv","dc_ze5o8drnl9"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Proposal gr_cuobjlny6r reaches Mitchell in the Town Hall in-tray on its own; nothing to queue until he decides it. Its first step waits on as_twlx52w3wm (Kelly 1, running)."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-11-02T02:29:51.390Z"
sessionId: "se_y9bju91fp9"
assignmentId: "as_zacorg03g5"
costUsd: 1.2043471999999995
tokens: 60217
turns: 28
createdAt: "2026-11-02T02:29:42.145Z"
updatedAt: "2026-11-02T02:29:51.390Z"
---
## What I did
Read the code on main dab5b9b (core meetings.ts, access.ts, lanes.ts, goals.ts, permissions/schema; server routes/town.ts; web oneOnOne.ts, AgentPanel.tsx, BuildingPanel.tsx, Places.tsx, hud.tsx, StatsPanel.tsx). Then filed proposal **gr_cuobjlny6r** against gl_bl_hzjw0z0zlz (450,000 tokens, due 2026-11-09), source mt_hlizi9wxxc decision 1. Nothing built. Plan recorded on topic page [dc_ckzkpsahhv](../../wiki/2026-10/2026-10-29-permissions-ask-to-join-member-kr-4-zkpsahhv.md).

## Findings
- **How it works today:**
  - Let in (`decideAccess`, access.ts:60-80) grants only the town `member` role, and only admins can do it.
  - A plain member gets only the default manager 1:1 (meetings.ts:213-215). The manager is told "don't take direction" by `oneOnOneMemberBlock` (meetings.ts:163-171, used at runtime manage.ts:213).
  - Calling a meeting needs facilitate or review rights in the building.
  - **Gap:** `humanSource` (lanes.ts:26-44) accepts any human's tell or any meeting with a human as the source for directed work. It never checks who that human is. The new gate has to close this, or "no permission" means nothing for directed work.
  - The User stats stand has no per-member rows yet, so the later grant needs a new Members table (GET /api/members).
- **Plan, in 3 steps (each one commit plus a live check):**
  1. Add a `direct_grants` table (migration 083) and a core check `canDirect`. It is true if the person reviews or facilitates in the building, captains the building's goal or a goal above it, or holds a grant on one of those goals. Use it for 1:1s, meeting calls and directed-work sources. Delete the member-only 1:1 path and the prompt block. Add grant and revoke endpoints, plus server tests.
  2. On the in-tray Let in card and the HUD notice, add "Let in + direct work under <goal>". Show the Talk button only to people who pass the server check, and delete the member callout.
  3. Add a Members table to User stats with one-click grant and revoke, plus a line in the manual.
- **Key results:** kr_v21y6z4tbv, kr_etn1l9ccpi, kr_qtmcpalo80, kr_t7rw103x6u, kr_3huiw2mea7.
- **Kept narrow:** approving join requests stays admin-only, because that's how `decideAccess` works today. Letting captains approve joins is out of scope unless Mitchell asks.
- **Depends on:** as_twlx52w3wm (removing the one-1:1-a-day cap) landing first.

## What I need from you
Fund, counter or reject gr_cuobjlny6r in the Town Hall in-tray.
