---
id: "dc_66xza1ey0x"
type: "report"
state: "building"
title: "Onboarding rollup: Members table (direct-work Grant/Revoke) live in 66e5d33; the join funnel's top step counts page loads, not people"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_51ptfuz2at"],"urls":["https://muster.town/api/join-funnel","https://github.com/mitchellgordon95/agent-town/commit/df1cb9e5"]}
tags: ["rollup"]
verdict: "continue"
decision: "pending"
sessionId: "se_74ckwzrxj7"
createdAt: "2026-11-03T18:03:18.571Z"
updatedAt: "2026-11-03T18:03:18.571Z"
---
Live: **66e5d33** since 2026-11-03 04:17 UTC. It contains df1cb9e5, the last step of gr_cuobjlny6r, which my checkpoint card (filed before that deploy) described as "on main, not yet live". No pictures: both items are API/code-verified; the card pictures are the held live checks.

## Shipped

**1. Members table on the user stats stand is live**
**What it is:** Town Hall → user stats → a Members section for an admin or captain: each let-in member, when they were let in, their direct-work goals as chips with Revoke (or "none"), and one primary Grant <goal> per member. Same permission the two-button Let in card gives at the door, now grantable or revokable later (df1cb9e5; code at packages/web/src/panels/StatsPanel.tsx:108).
**What you'd see:** Press E on the stats easel at the Town Hall and scroll past the join funnel. Today it lists the one let-in member. Verified from the code snapshot at the live commit; a live screenshot with Grant/Revoke pressed is the held check as_vpdz73pnlc, which runs if the grant continues.
**Your call:** None.

**2. The join funnel's top step can't be read as "people who saw the card"**
**What it is:** A finding, not a change ([dc_dmmktg7x3w](../../note/2026-11/2026-11-03-findings-the-join-funnel-s-top-step-can-t-be-trust-mktg7x3w.md)). The guest card sends one unauthenticated ping per page load with no visitor id (packages/web/src/hud.tsx:67), and the server adds 1 every time with no dedup or user-agent filter (packages/server/src/app.ts:197). Pressing Sign in is never counted: `GET /auth/github` records nothing, and `signIns` only counts new accounts. The homepage has no count at all.
**What you'd see:** /api/join-funnel, last 30 days: 212 guest-card views, 2 sign-ins, 1 asked, 1 let in, 0 acted. On the Workshop since 10-31: 205 views, 0 sign-ins. 105 of those views landed within about 2 h 15 min of the ping going live on 10-31, which is most likely our own headless live checks and reloads (an inference: the server keeps nothing that splits the count by source). So the funnel can't yet say whether strangers leave at the card or at GitHub's consent screen.
**Your call:** The fix is the 45k proposal already in your in-tray (distinct visitors per day via a hashed localStorage id, a signInStarted step, homeViews, all shown in User stats). Nothing else to decide here.

## Decided
- [dc_51ptfuz2at](2026-11-03-explore-the-join-funnel-s-top-step-counts-page-loa-ptfuz2at.md) → approve (exploration done; its proposal waits in the Town Hall in-tray; nothing queued)

## Key results
Grant figures are as of the gr_cuobjlny6r checkpoint card (no grant-lane work ran since; all four grants are held or checkpointed).

| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_cuobjlny6r | kr_v21y6z4tbv Let in card: one click lets in + grants direct work | claimed | 478,159 / 450,000 |
| gr_cuobjlny6r | kr_etn1l9ccpi Same grant/revoke from User stats | on-track (now live in 66e5d33; live press pending held check) | " |
| gr_cuobjlny6r | kr_qtmcpalo80 Non-holder: no Talk, no callout, 403 | claimed | " |
| gr_cuobjlny6r | kr_t7rw103x6u Holder 1:1 → directed assignment; acted +1 | on-track (needs a real stranger) | " |
| gr_cuobjlny6r | kr_3huiw2mea7 Gate tested, CI green | claimed | " |
| gr_fibsfwr4tz | kr_pxisdsocdp, kr_a32db87f39, kr_fbef01cccb, kr_4395ff116f funnel steps 1–3 | live, checked | 407,049 / 450,000 |
| gr_fibsfwr4tz | kr_bf2df18aa1 round trip | not done; final check scheduled 2026-11-07 21:00 UTC | " |
| gr_58n37j410s | kr_e13rgsded6 / kr_xqbhxxptf3 / kr_5xzxdvr1g5 | at-risk / on-track / on-track (at checkpoint, asked to cut) | 665,032 / 500,000 |
| gr_ngg1z160a8 | kr_z7sh9b4kxr, kr_9c3iz1ih4s / kr_mw367chfbp | claimed / on-track (at checkpoint) | 408,681 / 250,000 |

Spend today by lane: exploration 20,910 tokens (free under the goal: 9,504), directed 129 tokens.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 1 proposal (gr_zoo2cf2zpp), 4 requests ([dc_mgcbv3kqnd](../../../../../town-hall/outbox/2026-10/2026-10-31-one-real-join-round-trip-a-never-granted-github-ac-cbv3kqnd.md), [dc_ulla3hu21p](../../../../../town-hall/outbox/2026-11/2026-11-01-add-on-to-the-join-round-trip-dc-mgcbv3kqnd-after-la3hu21p.md), [dc_fvlt8xajnz](../../../../../town-hall/outbox/2026-11/2026-11-02-add-on-to-the-join-round-trip-dc-mgcbv3kqnd-after-lt8xajnz.md), [dc_wtz7ltq8hf](../../../../../town-hall/outbox/2026-11/2026-11-03-add-on-to-the-join-round-trip-dc-mgcbv3kqnd-let-in-z7ltq8hf.md)), 3 rollups ([dc_u74lxukm10](2026-11-02-onboarding-rollup-2026-11-02-help-signs-done-membe-4lxukm10.md), [dc_tmz3tm7jox](2026-11-03-checkpoint-for-gr-ngg1z160a8-founder-road-cap-line-z3tm7jox.md), [dc_xf0b06vatn](2026-11-03-checkpoint-for-gr-cuobjlny6r-direct-work-under-goa-0b06vatn.md))._
