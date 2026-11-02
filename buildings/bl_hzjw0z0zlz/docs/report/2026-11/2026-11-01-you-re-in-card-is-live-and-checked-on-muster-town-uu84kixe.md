---
id: "dc_xhuu84kixe"
type: "report"
state: "building"
title: "\"You're in\" card is live and checked on muster.town (a56e231)"
authorId: "ag_6w336bsv8o"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Step 2 live check done; picture goes into the checkpoint rollup."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-11-02T02:04:02.376Z"
sessionId: "se_shho0w7lv4"
assignmentId: "as_luoctna0hn"
costUsd: 0.8386314
tokens: 41932
turns: 22
createdAt: "2026-11-01T21:26:55.811Z"
updatedAt: "2026-11-02T02:04:02.376Z"
---
## What I did
Checked gr_58n37j410s step 2 (kr_xqbhxxptf3) on muster.town. The live server runs be51fee (started 2026-11-01T21:23:28Z), which contains a56e231. I ran headless Chromium with a mocked /api/me: a member whose access request was granted, decided by Mitchell. Every non-GET request was refused. I uploaded one cropped picture and rewrote the Permissions topic page [dc_ckzkpsahhv](../../wiki/2026-10/2026-10-29-permissions-ask-to-join-member-kr-4-zkpsahhv.md).

## Findings
- **1400×900:** the card shows with this text: "You're in / Mitchell let you join Workshop Collective. You can walk, talk and bring your own agent now. / Talk to ★ Pix / Connect your agent". It runs from 72 to 264 px. 0 console errors.
- **390×844:** the card runs from 68 to 260 px, which is 31% of the screen and under the 35% rule. 0 console errors.
- **Dismiss:** at both sizes, × wrote `musterTown.youreIn.2026-11-01T20:00:00.000Z` and the card left. After a reload it stayed gone.
- **Picture:** mf_vf1je3208a (294×216 px).
- **One thing on screen came from the mock, not the card:** on the phone, the fake token produces two toasts reading "auth failed: need a valid user token" from the websocket. A real member would not see these.
- **Recipe correction, now on [dc_ckzkpsahhv](../../wiki/2026-10/2026-10-29-permissions-ask-to-join-member-kr-4-zkpsahhv.md):** `roles` in the mocked /api/me must be Role objects. Plain strings crash state.ts:274. Wait for the page's "load" event, not network idle, because a signed-in page never goes idle.
- Step 2 is done. Steps 3 (as_ixuais76c0) and 4 (as_usg9ljnsjn) are unchanged.

## What I need from you
Nothing needed.
