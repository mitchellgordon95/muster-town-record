---
id: "dc_ph2l5w3c2q"
type: "report"
state: "building"
title: "Recurring key donations limited to N credits: live at f51fa0f, picture mf_u74ki6w79c, finance checks 15/15"
authorId: "ag_ts1s5f0vfb"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_uvbcl8tod6","dc_pnarp2er0m","mt_p3ge56kg03"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/216"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "PR #216 live at f51fa0f, picture mf_u74ki6w79c, check:finance 15/15. Chain as_v143vxiefm done; the directed item (mt_p3ge56kg03) goes in the next rollup with its \"Your call\" line. No further work."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-10-31T22:36:45.356Z"
sessionId: "se_osre4u8rel"
assignmentId: "as_1vtz85ct8n"
costUsd: 0.4034505000000001
tokens: 20173
turns: 11
createdAt: "2026-10-31T22:31:49.819Z"
updatedAt: "2026-10-31T22:36:45.356Z"
---
## What I did
- Confirmed that /api/health reports commit f51fa0f (server started 22:30:16Z).
- Took a picture of the live Donate form with ~/shots/donate-times.mjs. The script fakes the sign-in and aborts every POST, so no input was added.
- Ran `npm run check:finance` against muster.town.
- Rewrote the topic page [dc_pnarp2er0m](../../wiki/2026-10/2026-10-31-donate-spend-limit-line-for-pasted-api-keys-arp2er0m.md) to say the feature is LIVE.

## Findings
- PR #216 (recurring API-key donations limited to N credits) is live at **f51fa0f**. On the live form, with Daily and "A number of times" = 3, it shows "For how long", "Times (the first credit is now)" and the total line "3 × 1,000,000 = 3,000,000 adj. tokens over 3 days". Picture: **mf_u74ki6w79c** (467×180, cropped).
- `check:finance` at f51fa0f: all 15 checks pass with diff 0.
  - Daily inflow is still 11,500,000 adj. tokens/day, so the existing inputs are unchanged.
  - Bank balance is 512,250.
- I have not seen the "k of N credits left" line on a source card live, because no live input has a credit limit yet. Unit tests cover it (web 208/208).
- For the rollup: Mitchell asked for this Bank change himself in 1:1 mt_p3ge56kg03. Migration 074 only adds two nullable columns. This chain (as_v143vxiefm) is done.

## What I need from you
Nothing needed.
