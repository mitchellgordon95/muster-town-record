---
id: "dc_uje0xnxc2c"
type: "report"
state: "building"
title: "Onboarding rollup: the stranger account has asked to join (ar_ogi7no5l2v, your Let in is the next step); never-run collectives read \"Not started yet\" on the homepage; style guide carries your sidebar-vs-sheet rule"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_llbxzopol8","dc_rueh6o3mo1","dc_ndhlx95eno","dc_sniltaea7o","dc_a0qm0xiwxu"],"urls":[]}
tags: ["rollup"]
verdict: "stop"
decision: "pending"
sessionId: "se_driqwb4fqi"
assignmentId: "as_oplzqoksfw"
costUsd: 1.8588562499999999
tokens: 92943
turns: 17
createdAt: "2026-11-06T04:34:17.286Z"
updatedAt: "2026-11-06T04:34:17.286Z"
---
Live: **5dc50c70** (server started 2026-11-06 04:19:57Z, read from /api/health at 04:32:36Z). Your message via Pix ([dc_5bgy20qlvt](../../../../../library/human-report/2026-11/2026-11-06-re-create-a-second-github-account-for-testing-and-gy20qlvt.md)) is acted on: Pix answered.

## Shipped

**1. The test account has asked to join: the round trip is half done and waits on your click**
**What it is:** Onboarding ran the join round trip itself with the stranger account you added (dungeonrpg99-ops), no outbox request. Kelly 1 signed in with the token, confirmed the account is visitor-only, and filed Ask to join at 04:31:58Z (request ar_ogi7no5l2v, pending; the join funnel's asked count rose by one). The two old "test this for us" requests are withdrawn. Grant gr_fibsfwr4tz step 4, key result kr_pxisdsocdp.
**What you'd see:** Town Hall in-tray: "dungeonrpg99-ops asked to join" with Let in / Decline; HUD Notices shows the same with its age. Events: "asked to join" at 04:31:58Z. API-only so far, no picture.
**Your call:** Click Let in on dungeonrpg99-ops. Kelly 1 is parked on it and finishes the round trip (a Say from the account, then it frees the account for the Workshop's captain check).

**2. Never-run collectives say so on the homepage (48d88720, live)**
**What it is:** The homepage tile of a collective that has never run reads "Not started yet: waiting for its founder's key" instead of "Resting now", and sits after the ones that have run. The API says it too: /api/collectives carries started true/false per collective. Grant gr_a6512x0je1, two of three key results checked live on desk and phone, 0 console errors ([dc_rueh6o3mo1](2026-11-06-never-run-live-check-api-and-homepage-pass-trauma-eh6o3mo1.md)).
**What you'd see:** muster.town in a private window: Workshop tile first with its "working now" pill, then Hollyville and Trauma reading "Not started yet".
![Homepage tiles: Workshop first, Hollyville and Trauma "Not started yet"](/api/media/mf_yfjcuzpxsf.png)
**Your call:** None. The third key result (the /trauma/ guest card itself saying it hasn't started) failed live because the WebSocket snapshot schema stripped the started flag; the fix is commit 6f1f2005 on main, not yet deployed by CI at 04:32Z, and a re-check runs by itself once it is live.

**3. The style guide now carries your sidebar-vs-sheet rule**
**What it is:** The muster-style-guide skill ([dc_q736158pnn](../../skill/2026-10/2026-10-26-muster-style-guide-36158pnn.md)) has a new section 12 "Sidebars and sheets": a sidebar holds a list, navigation or a short detail; anything with its own id that you'd scroll opens in a centred sheet. Every line cites the code on main 5dc50c70. It is pinned for every Onboarding session and Teo was told (his kr_nokx342ovj).
**What you'd see:** Library or Onboarding filing cabinet: skill [dc_q736158pnn](../../skill/2026-10/2026-10-26-muster-style-guide-36158pnn.md), section 12. No picture (a document).
**Your call:** None.

## Decided
- [dc_llbxzopol8](2026-11-06-style-guide-skill-dc-q736158pnn-now-carries-mitche-bxzopol8.md) → approve (style-guide section 12 done)
- [dc_rueh6o3mo1](2026-11-06-never-run-live-check-api-and-homepage-pass-trauma-eh6o3mo1.md) → approve (two key results claimed; parked re-check as_5nt5nvead0 waits on 6f1f2005)
- [dc_ndhlx95eno](2026-11-06-grant-gr-fibsfwr4tz-adjusted-1-000-000-tokens-hlx95eno.md) → approve (gr_fibsfwr4tz adjusted to 1,000,000; step 4 running on it)
- [dc_sniltaea7o](2026-11-06-live-check-of-48d88720-handed-to-kelly-1-as-fjgpn4-iltaea7o.md) → approve (live check handed to Kelly 1)
- [dc_a0qm0xiwxu](2026-11-06-grant-gr-a6512x0je1-adjusted-1-000-000-tokens-qm0xiwxu.md) → approve (gr_a6512x0je1 adjusted to 1,000,000)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_fibsfwr4tz | kr_pxisdsocdp read-only stranger asks to join from the guest card | on-track: ask filed ar_ogi7no5l2v, Let in pending | 407,049 / 1,000,000 |
| gr_fibsfwr4tz | kr_a32db87f39 guest card promises only sign-in → Ask to join | not-started (steps 1–3 live; the fork claims it in its report) | |
| gr_fibsfwr4tz | kr_fbef01cccb join funnel counts public and moving | not-started (asked +1 seen at 04:32Z; claimed in the fork's report) | |
| gr_fibsfwr4tz | kr_4395ff116f pending request visible in HUD Notices with age | not-started (check on your side now) | |
| gr_fibsfwr4tz | kr_bf2df18aa1 real round trip done once | not-started: needs your Let in | |
| gr_a6512x0je1 | kr_6xv83q1k14 /api/collectives started flag | claimed ([dc_rueh6o3mo1](2026-11-06-never-run-live-check-api-and-homepage-pass-trauma-eh6o3mo1.md)) | 621,555 / 1,000,000 |
| gr_a6512x0je1 | kr_7pdn6k1w2r homepage tile "Not started yet", ordered after started ones | claimed (picture above) | |
| gr_a6512x0je1 | kr_fk7c0pdvvs never-run guest card says it hasn't started | at-risk: fix 6f1f2005 waiting on CI | |

Spend today by lane: exploration 0 tokens (free under the goal: 6,242,797); directed 228,623 tokens.

## Needs from Mitchell
1. Let in dungeonrpg99-ops (us_u4mzpz4zc7): Town Hall in-tray, Let in on its pending request ar_ogi7no5l2v. Kelly 1 is parked on that click and finishes the round trip the moment it lands; the Workshop's captain check on the same account waits behind it.

_Already waiting in your in-tray: 2 proposals (gr_uc179zv1xa, gr_y9bpvx197c), 0 requests, 0 rollups._
