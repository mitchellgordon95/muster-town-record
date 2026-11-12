---
id: "dc_ud8fgrr2z2"
type: "wiki"
state: "building"
title: "Chain rule (gr_2r17x8egrc step 1, kr_ig32y08ihi)"
authorId: "ag_pxke9xzdit"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "workshop"
createdAt: "2026-11-12T16:41:04.440Z"
updatedAt: "2026-11-12T16:41:04.440Z"
---
State on 2026-11-12, session as_zf4kr77hai (Pix 2).

- PR #436 open (draft), branch agent/pix-2/step-1-of-gr-2r17x8egrc-chain-rule-with-. Not merged, not live yet.
- What it does: core `Goals.chainConflict` / `requireChainFree` refuse a lab at, above or under an occupied goal in createBuilding, attach and adopt (root shared, Town Hall exempt). A human goal move may create an overlap; `goal.moved` records `chainOverlaps`. Boot (server main.ts, after the Secretary setup) appends one `system` event "chain audit: N violations, M accepted exceptions: …" (`Goals.logChainAudit`).
- Accepted exception = a human moved a goal between the two labs to where it is now (latest `goal.moved` on that goal, payload.by a user). UI / UX (bl_t7slw19vgg) under the Workshop: gl_bl_t7slw19vgg moved under gl_join by us_1la74k332n (Mitchell) 2026-10-31T04:16:54Z; kept by Mitchell's answer to ak_pzu7q469my.
- Simulated on the live tree (GET /api/goals, 16:5xZ): exactly one pair, UI / UX under Town Workshop. Expected boot line: "chain audit: 0 violations, 1 accepted exception".
- Next: merge #436 when green, park {deploy: sha}, read the system event (GET /api/events?types=system or the event log), claim kr_ig32y08ihi.
- Sources: plan [dc_q0838kcg6c](../../report/2026-11/2026-11-12-chain-rule-stopped-before-code-ui-ux-already-sits-838kcg6c.md), docs/goals.md "One building per chain".
