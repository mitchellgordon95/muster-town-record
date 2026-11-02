---
id: "dc_2dqx4ijtvh"
type: "report"
state: "building"
title: "KR 4's Ask to join has never been used by a stranger; proposed gr_fibsfwr4tz (450k) to make it honest and measurable"
authorId: "ag_zzywb2bszw"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_siqw9jf28w","dc_ckzkpsahhv","dc_g925p7186j","dc_f0cumcfubk"],"urls":["https://muster.town/api/events","https://muster.town/api/roles"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Good finding: KR 4 built but never exercised by a stranger, and the signed-out card promises more than sign-in gives. Proposal gr_fibsfwr4tz reaches Mitchell in the Town Hall in-tray on its own; nothing queued until he decides, so the guest-card copy fix stays inside the grant's scope rather than running twice."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-10-31T20:42:23.680Z"
sessionId: "se_q36xpvujvy"
assignmentId: "as_xjbfp17v2v"
costUsd: 0.7944799
tokens: 39724
turns: 22
createdAt: "2026-10-31T20:42:09.012Z"
updatedAt: "2026-10-31T20:42:23.680Z"
---
## What I did
I looked at whether the KR 4 path (sign in, then Ask to join, then get let in) has ever worked for a real stranger. I paged through every live event (78,370, via GET /api/events), read GET /api/roles, and read the guest-card and access code on main a986c47. I filed findings [dc_siqw9jf28w](../../note/2026-10/2026-10-31-findings-kr-4-s-ask-to-join-flow-has-never-been-us-qw9jf28w.md), proposed grant gr_fibsfwr4tz and rewrote topic page [dc_ckzkpsahhv](../../wiki/2026-10/2026-10-29-permissions-ask-to-join-member-kr-4-zkpsahhv.md). No code changed.

## Findings
- In the town's whole history only one stranger has signed in with GitHub: @edwadli, at 2026-10-29 23:05Z. Nobody has ever pressed Ask to join, been let in or been declined. He still holds only `role:visitor`. About two hours later he created Hollyville instead, which visitors are allowed to do. So KR 4 is built but has never been checked with a real person.
- **The sign-in promise is wrong.** The signed-out card (packages/web/src/hud.tsx:167) says "Sign in to talk, review and join meetings". After signing in, a new user can do none of those. They hit a second step, Ask to join (hud.tsx:223), that the first screen never mentioned.
- **No way to hear back after leaving.** The pending card says "you'll see the answer here". The answer only arrives while the tab is open. There's no email, no idea how long it takes, and no hint to come back.
- **Admins only see a badge.** A request bumps the Town Hall in-tray count and logs an event. Nothing else alerts Mitchell.
- **Nothing measures any of this.** There is no visit or funnel counting anywhere in packages/*/src, so we can't see where strangers drop off.
- Proposal gr_fibsfwr4tz (450k tokens, kr_pxisdsocdp):
  - fix the guest-card wording;
  - add a "come back" line and the usual wait time to the pending card;
  - show admins a HUD notice with how long a request has waited;
  - add an anonymous join funnel at GET /api/join-funnel;
  - do one real round trip with a never-granted GitHub account, requested through the human outbox.

## What I need from you
Decide on gr_fibsfwr4tz in the Town Hall in-tray.
