---
id: "dc_8t481sdm3e"
type: "report"
state: "building"
title: "Onboarding close rollup: gr_ngg1z160a8 (founder road) closed as done, all three key results live in db2b9dd; 62,692 tokens back to the Bank"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_raqqiz3nkj","dc_qns8vir3lf"],"urls":["https://muster.town/hollyville/api/health","https://muster.town/api/join-funnel"]}
tags: ["rollup"]
verdict: "continue"
decision: "pending"
sessionId: "se_arbqgw3tbn"
createdAt: "2026-11-04T00:26:08.927Z"
updatedAt: "2026-11-04T00:26:08.927Z"
---
Live: **db2b9dd** since 2026-11-04 00:24 UTC; it contains 58fc4834, the last step of gr_ngg1z160a8. No pictures: the live-check screenshots exist only on Kelly 1's desk (no upload tool); the notice texts are quoted below.

## Shipped

**1. gr_ngg1z160a8 closed as done: the founder HUD after the key is live and checked**
**What it is:** The last key result (kr_mw367chfbp). A hosted collective's /api/health now carries `founder: {exploringSince, proposals, funded}`, and the founder's HUD Notices say what their agents are doing until the first grant is funded: "Your agents are exploring <goal> (started Nm ago)", then "Your first proposal is waiting · Fund or reject →", then nothing once funded. The other two key results (the 1,000,000-token cap stated before pasting a key, with a server test; the public founder road in /api/join-funnel) were already claimed at the checkpoint. The close returned 62,692 unspent tokens to the Bank (437,308 of 500,000 spent).
**What you'd see:** Kelly 1 set each of the three founder states on muster.town/hollyville/ at 1400×900 and 390×844: all three render as quoted above, 0 console errors ([dc_raqqiz3nkj](2026-11-04-founder-hud-after-the-key-kr-mw367chfbp-is-live-an-qqiz3nkj.md)). /hollyville/api/health and /trauma/api/health both show `founder: {exploringSince: null, proposals: 0, funded: false}` today; the root Workshop /api/health has no such field, as intended.
**Your call:** Mark the three key results met or missed on the close card. One honest limit: no hosted collective has a key yet (hollyville since 10-29, trauma since 11-01, both keyAdded false), so the notices were checked with mocked states, not against a real founder's events; and nothing shows between pasting the key and the first exploration starting (the grant didn't ask for it). If you'd like that gap filled, say so and I'll propose it; otherwise nothing more.

## Decided
- [dc_raqqiz3nkj](2026-11-04-founder-hud-after-the-key-kr-mw367chfbp-is-live-an-qqiz3nkj.md) → approve (live check done; grant closed on its evidence; nothing queued)
- [dc_qns8vir3lf](2026-11-04-grant-gr-ngg1z160a8-adjusted-500-000-tokens-s8vir3lf.md) → approve (your continuation of gr_ngg1z160a8 to 500k; the held check ran and finished)

## Key results
gr_cuobjlny6r figures are as of your continuation at 00:21 UTC; its two live checks (Let in card pictures, Members table Grant/Revoke press) are running now and its close rollup follows when they report.

| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_ngg1z160a8 (closed, done) | kr_z7sh9b4kxr cap stated before the key | claimed | 437,308 / 500,000 |
| gr_ngg1z160a8 | kr_9c3iz1ih4s founder road counted in public | claimed | " |
| gr_ngg1z160a8 | kr_mw367chfbp HUD names the next thing after the key | claimed (this rollup) | " |
| gr_cuobjlny6r | kr_v21y6z4tbv Let in card: one click lets in + grants direct work | claimed | 746,644 / 1,500,000 |
| gr_cuobjlny6r | kr_etn1l9ccpi Same grant/revoke from User stats | on-track (live in 66e5d33; press check running) | " |
| gr_cuobjlny6r | kr_qtmcpalo80 Non-holder: no Talk, no callout, 403 | claimed | " |
| gr_cuobjlny6r | kr_t7rw103x6u Holder 1:1 → directed assignment; acted +1 | on-track (needs a real stranger) | " |
| gr_cuobjlny6r | kr_3huiw2mea7 Gate tested, CI green | claimed | " |
| gr_fibsfwr4tz | kr_pxisdsocdp, kr_a32db87f39, kr_fbef01cccb, kr_4395ff116f funnel steps 1–3 | live, checked | 407,049 / 450,000 |
| gr_fibsfwr4tz | kr_bf2df18aa1 round trip | not done; final check scheduled 2026-11-07 21:00 UTC | " |
| gr_58n37j410s | kr_e13rgsded6 / kr_xqbhxxptf3 / kr_5xzxdvr1g5 | at-risk / on-track / on-track (at checkpoint, asked to cut) | 665,032 / 500,000 |

Spend today by lane: exploration 0 tokens (free under the goal: 0), directed 0 tokens.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 1 proposal (gr_zoo2cf2zpp), 4 requests ([dc_mgcbv3kqnd](../../../../../town-hall/outbox/2026-10/2026-10-31-one-real-join-round-trip-a-never-granted-github-ac-cbv3kqnd.md), [dc_ulla3hu21p](../../../../../town-hall/outbox/2026-11/2026-11-01-add-on-to-the-join-round-trip-dc-mgcbv3kqnd-after-la3hu21p.md), [dc_fvlt8xajnz](../../../../../town-hall/outbox/2026-11/2026-11-02-add-on-to-the-join-round-trip-dc-mgcbv3kqnd-after-lt8xajnz.md), [dc_wtz7ltq8hf](../../../../../town-hall/outbox/2026-11/2026-11-03-add-on-to-the-join-round-trip-dc-mgcbv3kqnd-let-in-z7ltq8hf.md)), 4 rollups ([dc_u74lxukm10](2026-11-02-onboarding-rollup-2026-11-02-help-signs-done-membe-4lxukm10.md), [dc_tmz3tm7jox](2026-11-03-checkpoint-for-gr-ngg1z160a8-founder-road-cap-line-z3tm7jox.md), [dc_xf0b06vatn](2026-11-03-checkpoint-for-gr-cuobjlny6r-direct-work-under-goa-0b06vatn.md), [dc_66xza1ey0x](2026-11-03-onboarding-rollup-members-table-direct-work-grant-xza1ey0x.md))._
