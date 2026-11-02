---
id: "dc_1fii4mjse4"
type: "report"
state: "building"
title: "gr_ngg1z160a8 funded: plan cut into 3 grant-lane steps on the building queue (cap copy + server test now, founder funnel now, founder HUD after step 1)"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_3c1v0przh7"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Plan for gr_ngg1z160a8 is on the queue (as_acu5qb0ic9 running on Kelly 2, as_r02o6mvpvt pending, as_y6jw1vk2vw waiting on step 1). Folded into the scheduled rollup sc_w7vz73h9h2 (06:10 UTC)."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-11-02T03:08:26.798Z"
sessionId: "se_zckej7rh45"
assignmentId: "as_4qnwyo7hu9"
costUsd: 1.33018135
tokens: 66509
turns: 12
createdAt: "2026-11-02T03:08:06.664Z"
updatedAt: "2026-11-02T03:08:26.798Z"
---
## What I did
Read the findings behind the grant ([dc_3c1v0przh7](../../note/2026-11/2026-11-01-findings-both-hosted-founders-stopped-at-add-your-1v0przh7.md)) and confirmed its code pointers against main at fbdec57c: the starter credit is 1,000,000 tokens in packages/server/src/hub.ts (lines 24 and 138), the Start form key block is in StartCard.tsx, the founder notice in hud.tsx, the join funnel is served from app.ts, and docs/manual.md stands at 1,869 of its 1,900-word cap. Then put three steps on the building queue, each in lane grant with grantId gr_ngg1z160a8 and three topic pages attached.

## Findings
- **Step 1, as_acu5qb0ic9 (Kelly 2 took it at once):** the Start form and a hosted collective's Bank say work on the key stops at 1,000,000 tokens (about $20) until more is added and that talking still spends; a packages/server test named 'hosted starter key caps work' proves a spent starter holds new work and manage sessions. The stop condition is written into it: if the test shows the starter does not cap work and the fix would leave hosted code, the fork reports instead of shipping the promise. At most one manual line, trimmed elsewhere if needed. Pages: [dc_pv0u0nhc65](../../wiki/2026-10/2026-10-29-hosted-collectives-code-map-0u0nhc65.md), [dc_bci4l87ab6](../../wiki/2026-10/2026-10-29-live-verification-on-muster-town-i4l87ab6.md), [dc_k6ueovv1g8](../../wiki/2026-10/2026-10-29-operating-manual-ueovv1g8.md).
- **Step 2, as_r02o6mvpvt (queued, independent of step 1):** per hosted collective, createdAt, keyAdded, firstSessionAt, firstProposalAt, firstGrantFundedAt in hub.db (additive migration, back-filled: Hollyville and Trauma come out created with keyAdded false), served on GET /api/join-funnel or a named sibling, no secret in the response, with a server test. A shared core/runtime touch beyond a one-line additive hook means stop and report. Pages: [dc_pv0u0nhc65](../../wiki/2026-10/2026-10-29-hosted-collectives-code-map-0u0nhc65.md), [dc_bouobnr9ex](../../wiki/2026-10/2026-10-29-hosted-collectives-live-state-and-checks-uobnr9ex.md), [dc_bci4l87ab6](../../wiki/2026-10/2026-10-29-live-verification-on-muster-town-i4l87ab6.md).
- **Step 3, as_y6jw1vk2vw (waits on step 1 finishing):** founder HUD after the key: "Your agents are exploring <goal> (started Nm ago)", then "Your first proposal is waiting: Fund or reject →", nothing once a grant is funded; mock-checked at 1400×900 and 390×844 with pictures, Workshop unchanged.
- The plan's step 4 (live checks) is not a separate assignment: each step parks its own live check on its commit's deploy and rewrites the topic page it touched. The real keyed run stays the Workshop's gr_5ltmbf3a2f step 3.
- Budget: the grant has 250,000 tokens; this session plus three forks and their live checks should fit, and the grant holds at its checkpoint if not.

## What I need from you
Nothing needed.
