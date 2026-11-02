---
id: "dc_4ml9fl8s9s"
type: "report"
state: "building"
title: "Workshop rollup 18: both of your flags are live (planner desks, standing flags), wake step 4 live, objectives/KPIs design on main. Mitchell: plant one flag to test pick-up, and mark up the draft objectives if you want changes"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_chw7ofjl7l","dc_gp9s9vi4vb","dc_g25kbxygmp","dc_kzzdspoith","dc_ykgewidnhn"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"Town Hall town-hall\": Workshop: FLY_DESKS_ACCESS_TOKEN is now granted town-wide. Pix assigns Root the image:true redeploy and the check that desk sessions post real token counters. T"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T17:42:52.853Z"
sessionId: "se_din5uffbr8"
createdAt: "2026-10-27T06:33:39.420Z"
updatedAt: "2026-10-27T17:42:52.853Z"
---
Since rollup 17 ([dc_grs5xrzok4](2026-10-27-workshop-rollup-17-draft-format-round-2-of-2-wake-s5xrzok4.md), 05:51Z, still undecided; its two wake checks and the grant top-up are still open). Live commit at 06:32Z: 49aeb33. No screenshots: this session had no desk.

## Shipped
Live in 49aeb33:
- **Your flag "town planner: auto-scale desks; number input stuck at zero"** ([dc_jv8q0ll5xh](../../flag/2026-10/2026-10-27-in-the-town-planner-let-s-auto-scale-desks-with-si-8q0ll5xh.md)): 0ff2338, Lena [dc_chw7ofjl7l](2026-10-27-planner-desks-now-follow-the-building-s-size-and-n-w7ofjl7l.md). Desks follow the size you draw or resize; the desks and max-turns boxes can be emptied while typing. Try: open the planner, draw a building, watch the desk count follow; clear the desks box.
- **Your flag "flags visibly planted; manager walks over to pick it up"** ([dc_r40dq3znse](../../flag/2026-10/2026-10-27-oh-also-flags-should-also-be-visibly-planted-in-th-0dq3znse.md)): faed70b, Root [dc_6443yq7aw4](2026-10-27-planted-flags-now-stand-on-the-map-until-the-manag-43yq7aw4.md), live check [dc_ykgewidnhn](2026-10-27-faed70b-is-live-flags-are-in-api-town-and-the-red-gewidnhn.md). A flag you plant now stands as a red pennant on your tile; I walk to it and pick it up to read it; you still decide flags from the in-tray without walking. Your two earlier flags were planted before this landed, so they have no position. Not yet seen live: a planted flag with a position (needs item 1).
- **Wake step 4**: one Waker over the event log with its cursor stored in meta, Keel [dc_g25kbxygmp](2026-10-27-wake-step-4-is-on-main-as-49aeb33-runtime-130-130-5kbxygmp.md) (runtime suite 130/130, core wakes 14/14). Live but the live check (cursor advances, wakes still fire) is Keel's next session; it resumes by itself.
- **Objectives and KPIs design** (your 1:1 decisions 1-4): 6f023c4, docs only, Lena [dc_gp9s9vi4vb](2026-10-27-objectives-and-kpis-design-pushed-to-main-6f023c4-9s9vi4vb.md). Town KPIs Fund, Join, Trust at the top of a town dashboard; up to 3 objectives per building, key results under them; grants, lanes and checkpoints unchanged. Workshop draft objectives are in docs/goal-directed-budgets.md (needs item 2). Build starts next session: migration 043, kpis, set_objective, grouping, Dashboard panel.

On main, not yet live: **several open grant proposals per building** (ee536a5, Root [dc_kzzdspoith](2026-10-27-several-grant-proposals-can-now-be-open-per-buildi-zdspoith.md)): each proposal is funded, countered or rejected on its own; the in-tray already shows one row per grant. Root checks it live after the redeploy.

## Decided
- [dc_chw7ofjl7l](2026-10-27-planner-desks-now-follow-the-building-s-size-and-n-w7ofjl7l.md) (Lena, planner) → approve, done.
- [dc_gp9s9vi4vb](2026-10-27-objectives-and-kpis-design-pushed-to-main-6f023c4-9s9vi4vb.md) (Lena, objectives design) → approve; no markup from me, she builds what is written.
- [dc_g25kbxygmp](2026-10-27-wake-step-4-is-on-main-as-49aeb33-runtime-130-130-5kbxygmp.md) (Keel, wake step 4) → approve; parked for the live check.
- [dc_kzzdspoith](2026-10-27-several-grant-proposals-can-now-be-open-per-buildi-zdspoith.md) (Root, parallel proposals) → approve; I took the follow-up myself (as_0bfgrzg0u5, after ee536a5 is live): write two Workshop key results under the draft objectives (one Trust, one Join or Fund) and propose a modest grant for each, so the in-tray check has two proposals. Both key results and both proposals will be listed in rollup 19 for you to keep or cut.
- [dc_ykgewidnhn](2026-10-27-faed70b-is-live-flags-are-in-api-town-and-the-red-gewidnhn.md) (Root, flags live check) → approve; the pick-up check waits on a planted flag.

## Key results
- kr_vyrhhiyotb (Bank counts adjusted output tokens): on-track. gr_iq5m7dug56: 1,640,037 / 1,666,667 adjusted tokens (98.4%); it reaches the 100% checkpoint within about 27k tokens and then holds. The adjust to about 2.0M you agreed at the town hall (so the 7-day zero-deaths watch to 11-03 fits) is still not done.
- Spend today by lane: exploration 286,538 / 828,571; directed 1,455,849 (your flags, the wake system, the 1:1 work).

## Needs from Mitchell
1. Plant one flag on the map (press F while standing on a walkable tile), with any real request in it: that checks the standing flag and my pick-up, and the request gets done. The top-up of gr_iq5m7dug56 and the two wake checks from rollup 17 are still open.
2. Mark up docs/goal-directed-budgets.md "Objectives and KPIs" (the Workshop draft objectives, the Trust measure) only if you want changes before Lena builds; no reply means she builds it as written.
