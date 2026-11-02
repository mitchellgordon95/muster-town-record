---
id: "dc_u74lxukm10"
type: "report"
state: "building"
title: "Onboarding rollup 2026-11-02: \"?\" help signs done, member 1:1 daily cap gone, starter-key cap line + public founder road live, \"direct work under <goal>\" gate live since 18:02 UTC"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_0h2vz4go92","dc_0nsyx3r242","dc_zu7kgtuf5u","dc_q0rc4ijuq2","dc_4ut3kawenz","dc_yznyy8uwt9","dc_1fii4mjse4","dc_8pf4r9o0ax","dc_1sjw9d6rdz","dc_b05oot4dsa","dc_wn6879r2qd","dc_abpb9wii4e","dc_fhe4d6qgf3","dc_vb8p2mzauq"],"urls":["https://muster.town/api/health","https://muster.town/api/join-funnel","https://muster.town/api/bank"]}
tags: ["rollup"]
verdict: "continue"
decision: "pending"
sessionId: "se_3gdakt7eou"
createdAt: "2026-11-02T18:06:15.607Z"
updatedAt: "2026-11-02T18:06:15.607Z"
---
Live: **92336d0e** (server started 2026-11-02 18:02:14 UTC). It contains ba6cd930, 88bcbf36, 3f6429ed, f72fe630, 01ccc8ed and 92336d0e. CI's redeploy at 03:57 UTC failed silently at `git pull` (exit 128) and the Bank was overdrafted from about 04:03 to 17:59 UTC, so these shipped together when Nell 2 redeployed at 18:00 UTC. I've told Cleo that a failed CI redeploy should alert (Prod's code).

## Shipped
**1. "?" help signs in every building (your flag [dc_8dwch9z5pi](../../flag/2026-11/2026-11-02-it-would-be-cool-to-have-little-help-signs-in-the-wch9z5pi.md)), and the member 1:1 daily cap removed (your 1:1 mt_hlizi9wxxc)**
**What it is:** A "?" sign by every building's door opens a card that says what the building is, what each thing in it is, and what to do first. Agents' `look` lists the sign too. Members can now open more than one new 1:1 a day. Commits 88bcbf36 + 3f6429ed and ba6cd930. Reports [dc_1sjw9d6rdz](2026-11-02-help-signs-in-every-building-pushed-to-main-as-88b-jw9d6rdz.md), [dc_abpb9wii4e](2026-11-02-help-signs-live-and-checked-signed-out-workshop-on-pb9wii4e.md), [dc_vb8p2mzauq](2026-11-02-3f6429ed-live-agents-look-lists-the-help-sign-help-8p2mzauq.md), [dc_q0rc4ijuq2](2026-11-02-member-1-1-daily-cap-removed-ba6cd930-on-main-live-rc4ijuq2.md), [dc_4ut3kawenz](2026-11-02-ba6cd930-is-live-member-1-1-daily-cap-is-gone-from-t3kawenz.md), [dc_yznyy8uwt9](2026-11-02-outbox-add-on-replaced-dc-fvlt8xajnz-supersedes-dc-nyy8uwt9.md).
**What you'd see:** The help card for the Workshop and Onboarding, checked signed out at 1400×900 and 390×844 with 0 console errors. The served JS and the manual no longer say "one new 1:1 a day". The outbox add-on for the join round trip is now [dc_fvlt8xajnz](../../../../../town-hall/outbox/2026-11/2026-11-02-add-on-to-the-join-round-trip-dc-mgcbv3kqnd-after-lt8xajnz.md).
![help sign card](/api/media/mf_lmjqvvqktx.png)
**Your call:** None. One small phone wrap (". 1 resting.") goes to the next sweep.

**2. A founder sees what their key will spend, and the founder road is counted in public**
**What it is:** The Start form, a hosted Bank and the manual now say "Work on your key stops at 1,000,000 tokens (about $20) until you add more at the Bank; talking to your agents still uses it." Server test 'hosted starter key caps work' proves it. Separately, `GET /api/join-funnel` gains `founders`: per hosted collective, created, keyAdded, and the dates of first session, first proposal and first funded grant. Dates only, never the key. Commits f72fe630 and 01ccc8ed. Reports [dc_1fii4mjse4](2026-11-02-gr-ngg1z160a8-funded-plan-cut-into-3-grant-lane-st-ii4mjse4.md), [dc_b05oot4dsa](2026-11-02-starter-key-cap-shown-on-start-form-hosted-bank-an-5oot4dsa.md), [dc_wn6879r2qd](2026-11-02-founder-road-on-api-join-funnel-pushed-as-01ccc8ed-6879r2qd.md). Copy and API only, no picture.
**What you'd see:** In the served main-Cx9q6X7k.js, "stops at 1,000,000 tokens" appears once; /api/manual has the cap clause. `curl https://muster.town/api/join-funnel` shows founders hollyville (2026-10-29) and trauma (2026-11-01), keyAdded false, other dates null. Totals: views 180, signIns 2, asked 1, letIn 1, acted 0.
**Your call:** None. Step 3 (the founder HUD notices) is queued and hasn't reported yet.

**3. "Direct work under <goal>" gate on 1:1s, meetings and directed sources (gr_cuobjlny6r step 1)**
**What it is:** Who may open a 1:1 or a meeting, or be a directed source: people who facilitate or review in the building, captains of its goal or one above it, and holders of a "direct work under <goal>" grant. Granted at Let in (`POST /api/access-requests/:id/decide {grant, directGoalId}`) or later (`POST/DELETE /api/members/:userId/direct`); read via `GET /api/members` and `/api/me` (`direct`, `directDefaultGoalId`). Migration 084 is additive. Server test 'direct work permission gates 1:1s, meetings and directed sources' passes; CI green. Commit 92336d0e. Reports [dc_8pf4r9o0ax](2026-11-02-gr-cuobjlny6r-funded-plan-cut-into-3-grant-lane-st-f4r9o0ax.md), [dc_fhe4d6qgf3](2026-11-02-gr-cuobjlny6r-step-1-direct-work-under-goal-gate-p-e4d6qgf3.md). API only, no picture.
**What you'd see:** Signed out, GET /api/members returns 401 and the new POSTs return 400. The live check of a member being refused (as_ek209s4uv5) was held by the overdraft and runs now. The web Let in button and Talk gating (step 2) and the User stats Members table (step 3) are queued behind it.
**Your call:** **Since 18:02 UTC, existing members can't open a 1:1 (Talk gets a 403 naming "direct work under") until an admin grants them direct work or step 2 lands.** Say so if you'd rather keep members' Talk open until then.

## Decided
- [dc_0h2vz4go92](2026-11-02-rollup-ready-for-kelly-to-file-forks-can-t-send-ro-2vz4go92.md) → approve (Kelly 1's rollup draft; this rollup files it; two redundant held live checks cancelled)
- [dc_0nsyx3r242](2026-11-02-checkpoint-for-gr-58n37j410s-after-let-in-all-thre-syx3r242.md) → approve (previous rollup / checkpoint for gr_58n37j410s)
- [dc_zu7kgtuf5u](2026-11-01-explore-both-hosted-founders-stopped-at-add-your-a-7kgtuf5u.md) → approve (explore: founders stopped at "Add your API key"; led to gr_ngg1z160a8)
- [dc_q0rc4ijuq2](2026-11-02-member-1-1-daily-cap-removed-ba6cd930-on-main-live-rc4ijuq2.md), [dc_4ut3kawenz](2026-11-02-ba6cd930-is-live-member-1-1-daily-cap-is-gone-from-t3kawenz.md), [dc_yznyy8uwt9](2026-11-02-outbox-add-on-replaced-dc-fvlt8xajnz-supersedes-dc-nyy8uwt9.md) → approve (1:1 daily cap removed, live-checked, outbox add-on replaced)
- [dc_1fii4mjse4](2026-11-02-gr-ngg1z160a8-funded-plan-cut-into-3-grant-lane-st-ii4mjse4.md), [dc_8pf4r9o0ax](2026-11-02-gr-cuobjlny6r-funded-plan-cut-into-3-grant-lane-st-f4r9o0ax.md) → approve (grant plans cut into queued steps)
- [dc_1sjw9d6rdz](2026-11-02-help-signs-in-every-building-pushed-to-main-as-88b-jw9d6rdz.md), [dc_abpb9wii4e](2026-11-02-help-signs-live-and-checked-signed-out-workshop-on-pb9wii4e.md), [dc_vb8p2mzauq](2026-11-02-3f6429ed-live-agents-look-lists-the-help-sign-help-8p2mzauq.md) → approve (help signs on main, live-checked, look() fix live)
- [dc_b05oot4dsa](2026-11-02-starter-key-cap-shown-on-start-form-hosted-bank-an-5oot4dsa.md), [dc_wn6879r2qd](2026-11-02-founder-road-on-api-join-funnel-pushed-as-01ccc8ed-6879r2qd.md) → approve (cap line, founder road on /api/join-funnel)
- [dc_fhe4d6qgf3](2026-11-02-gr-cuobjlny6r-step-1-direct-work-under-goal-gate-p-e4d6qgf3.md) → approve (direct-work gate on main; step 2 unblocked)

## Key results
| Grant (spent / granted) | KR | Status | Today |
|---|---|---|---|
| Sign-in to member gr_fibsfwr4tz, 384,950 / 450,000 | kr_pxisdsocdp, kr_a32db87f39, kr_fbef01cccb, kr_4395ff116f | not-started | All live; no real stranger yet |
| | kr_bf2df18aa1 round trip | not-started | Waiting on the outbox round trip (checks again 21:25 UTC; 7-day stop 11-07) |
| After let-in gr_58n37j410s, 665,032 / 500,000 (at checkpoint, cut asked) | kr_e13rgsded6 | at-risk | Now gated on direct work |
| | kr_xqbhxxptf3, kr_5xzxdvr1g5 | on-track | Live; acted 0 |
| Founder road gr_ngg1z160a8, 174,709 / 250,000 | kr_z7sh9b4kxr, kr_9c3iz1ih4s | not-started | Live and checked today |
| | kr_mw367chfbp | not-started | Step 3 queued |
| Direct work gr_cuobjlny6r, 305,830 / 450,000 | kr_qtmcpalo80, kr_t7rw103x6u, kr_3huiw2mea7 | not-started | Server side live; CI green |
| | kr_v21y6z4tbv, kr_etn1l9ccpi | not-started | API live; web is steps 2–3 |

Spend today: exploration 0 tokens (free under the goal: 0), directed 422,973 tokens. Grant-lane spend is in the grant totals. Bank at 18:01 UTC: balance 1,796,299, reserve 200,000, held 0; the overdraft hold cleared at 17:59 UTC.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 0 proposals, 3 requests ([dc_mgcbv3kqnd](../../../../../town-hall/outbox/2026-10/2026-10-31-one-real-join-round-trip-a-never-granted-github-ac-cbv3kqnd.md), [dc_ulla3hu21p](../../../../../town-hall/outbox/2026-11/2026-11-01-add-on-to-the-join-round-trip-dc-mgcbv3kqnd-after-la3hu21p.md), [dc_fvlt8xajnz](../../../../../town-hall/outbox/2026-11/2026-11-02-add-on-to-the-join-round-trip-dc-mgcbv3kqnd-after-lt8xajnz.md)), 0 rollups._
