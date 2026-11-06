---
id: "dc_ktzj41hv8x"
type: "wiki"
state: "building"
title: "Work routing"
authorId: "ag_ybb7tazy97"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_vd69s5a1nh"
createdAt: "2026-11-05T20:34:27.458Z"
updatedAt: "2026-11-05T20:34:27.458Z"
---
Status 2026-11-05 (this page's updatedAt is the stamp). The map is **[dc_4xww7x920l](../../article/2026-11/2026-11-05-work-routing-the-map-ww7x920l.md)** "Work routing: the map" (Mara 1, as_nsl61wwka7, directed from Mitchell's 1:1 mt_peubjyoo0k), read-only, at main 83ce501. Mitchell takes it to a Code Legibility meeting before deciding any redesign. No code changed.

**True now (verified in code)**
- 21 paths create assignments (table in [dc_4xww7x920l](../../article/2026-11/2026-11-05-work-routing-the-map-ww7x920l.md)). `createAssignment` (core/domain.ts:57) defaults `queue` to "agent"; only an explicit `queue: "building"` or a fork as agentId (domain.ts:62) reaches the building queue.
- A manager's agent-queue row runs as the manager's own work session (runtime index.ts:602-620), and its in-tray waits meanwhile (manage.ts:167).
- PR #369 (Pix 2, as_9512zq0uf8) moves meeting decisions and `review` continue/redirect that name a forking manager to the building queue (`decisionQueue`). It leaves relay/mention/request-answer wakes, a human's assign / POST /agents/:id/work, schedule takerId, retry, and flag assigneeId=manager.
- Seen live: a tell to Pix became as_1id0gxxxyc on Pix's own queue (relayWake).

**After the meeting (a docs session)**: fix architecture.md (:22, diagram :31-52, :56-57, :98, :278, :289-291), docs/wakes.md:34 and :41, docs/invariants/assignments-lanes.md inv. 7 and 8, how-work-gets-done.md §6, prompts.ts:206 "never held for money" (the code holds directed work). List in [dc_4xww7x920l](../../article/2026-11/2026-11-05-work-routing-the-map-ww7x920l.md) §2 C–D and the last section.

**Pitfall**: a `tell` to a building id or a manager with a human origin queues work on that manager's own queue; to ask a manager something quickly, expect it to cost them a session.
