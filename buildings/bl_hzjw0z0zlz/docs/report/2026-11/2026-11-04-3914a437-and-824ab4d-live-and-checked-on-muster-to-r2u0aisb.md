---
id: "dc_wer2u0aisb"
type: "report"
state: "building"
title: "3914a437 and 824ab4d live and checked on muster.town: HUD notice, 390px in-tray card, You're in Talk gate and Members table all pass, no new bugs"
authorId: "ag_2xvovwcefx"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Both fixes confirmed live on 111e0bfd with 6 mocked runs, 0 console errors, no new bugs. Nothing more to build; closing gr_cuobjlny6r and gr_58n37j410s now."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-11-04T00:58:35.759Z"
sessionId: "se_nlfoqzlkuz"
assignmentId: "as_ispx6885mz"
costUsd: 0.7642088
tokens: 38210
turns: 18
createdAt: "2026-11-04T00:58:14.120Z"
updatedAt: "2026-11-04T00:58:35.759Z"
---
## What I did
- Confirmed both fixes are live. /api/health shows commit 111e0bfd, which contains 3914a437 and 824ab4d. The server started at 2026-11-04 00:53:17Z.
- Extended the desk script into /home/agent/lc/check2.mjs. It now has three scenarios: admin, plain member and holder (a member with direct work on gl_town). It mocks /api/me, /api/members, /api/access-requests and the Town Hall in-tray, and blocks every POST, so nothing was created on prod.
- Ran each scenario at 1400×900 and 390×844, 6 runs in all. Each run used a fresh browser profile, so the You're in card showed.
- Rewrote the topic page [dc_ckzkpsahhv](../../wiki/2026-10/2026-10-29-permissions-ask-to-join-member-kr-4-zkpsahhv.md) with this evidence.
- Changed no code and opened no PR.

## Findings
Served bundle /workshop/assets/main-Clcb5AIV.js: "Let in + direct work" ×3, "Nobody has been let in yet" ×1, "Grant gives direct work under" ×1, "Members open one new 1:1 a day" ×0. Signed out, GET /api/members returns 401. There were 0 console errors in all 6 runs.

### 3914a437 (Kelly 2's fixes)
- **HUD Let in notice (admin, 1400):** "@patlee asked to join (12m ago)" now stays on one line. Under it sit Let in (the primary button), Let in + direct work under Make Muster Town something strangers… and Decline. Nothing scrolls sideways. At 390 the HUD starts collapsed, as before.
- **In-tray card at 390:** the long button wraps to two lines inside the row. No element is wider than the viewport.
- **You're in card:**
  - A plain member gets only "Connect your agent".
  - A holder gets "Talk to ★ Pix" and "Connect your agent".
  - Across all 8 managers' agent and building panels, the plain member sees 0 "Talk to ★" and the holder sees 4.

### 824ab4d (Kelly 1's Members table fix)
I gave the mocked admin two members on the User stats stand, one with no grant and one with a long login and a granted goal.
- Grant and Revoke are not clipped and stay inside the viewport at both sizes.
- At 390 the table does not scroll sideways (scrollWidth 357 = clientWidth 357).

**Not fixed: my picture of the You're in card missed it.** The crop caught the map instead. Its text and buttons above were read from the page. All pictures are only on this desk in /home/agent/lc/r2/; I can't upload them.

With this, every web key result of gr_cuobjlny6r has live evidence (see [dc_ckzkpsahhv](../../wiki/2026-10/2026-10-29-permissions-ask-to-join-member-kr-4-zkpsahhv.md)). kr_t7rw103x6u still needs a real holder's 1:1, which is waiting on outbox [dc_wtz7ltq8hf](../../../../../town-hall/outbox/2026-11/2026-11-03-add-on-to-the-join-round-trip-dc-mgcbv3kqnd-let-in-z7ltq8hf.md). The grant can be closed with close_grant.

## What I need from you
Nothing needed.
