---
id: "dc_btkb944omb"
type: "report"
state: "building"
title: "Workshop rollup 20: desk image push still blocked on FLY_DESKS_ACCESS_TOKEN (needs a Fly secret deploy from you); objectives, grouped views and side-by-side proposals verified live on 6c80fe4/4be312e"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_m3hubfy16p","dc_4qr0mgg2tg","dc_5wmk3a17hf"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"Town Hall town-hall\": Workshop: FLY_DESKS_ACCESS_TOKEN is now granted town-wide. Pix assigns Root the image:true redeploy and the check that desk sessions post real token counters. T"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T17:42:52.862Z"
sessionId: "se_ys96xgktvx"
createdAt: "2026-10-27T09:02:18.686Z"
updatedAt: "2026-10-27T17:42:52.862Z"
---
## Shipped
- **Grouped views verified live** (Lena, [dc_4qr0mgg2tg](2026-10-27-6c80fe4-live-the-workshop-s-three-objectives-group-r0mgg2tg.md), 6c80fe4): with the Workshop's three objectives entered, the board JSON, the guest board panel, the desk brief and the Dashboard all group key results under their objective correctly. Only the Building → Settings objectives editor is unverified: it is gated on building.manage, so it needs your one glance.
- **Two open proposals from one building side by side verified live** (Root, [dc_5wmk3a17hf](2026-10-27-two-workshop-proposals-are-open-side-by-side-on-th-mk3a17hf.md), mock 4be312e, CI green): the Workshop board lists both gr_f5bmciloqy and gr_tvt32g9xly in proposals[], the Town Hall in-tray shows each on its own row, and the desk brief names both. The counter path (answering one counter while the other stays open) still needs a human to counter one.
- Nothing new on main since 4be312e; the live commit is 4be312e.

## Decided
- [dc_4qr0mgg2tg](2026-10-27-6c80fe4-live-the-workshop-s-three-objectives-group-r0mgg2tg.md) (Lena, grouped views live check): approved; done.
- [dc_5wmk3a17hf](2026-10-27-two-workshop-proposals-are-open-side-by-side-on-th-mk3a17hf.md) (Root, side-by-side proposals live check): approved; done.
- [dc_m3hubfy16p](2026-10-27-fly-desks-access-token-still-missing-on-the-live-s-hubfy16p.md) (Root, desk image push re-check): approved. His redeploy with image:true at 09:00Z was skipped again: "no desk-app deploy token, FLY_DESKS_ACCESS_TOKEN". Every redeploy restarts node inside the same Fly Machine, so a staged secret never reaches the process; no Machine restart has happened since the secret was set. Desks are therefore still on the old image and their sessions still back-fill token counters (input 0, cacheWrite5m 0), while in-server sessions post real five-counter figures. Root gets the image:true redeploy and check as soon as you say the secret is deployed.
- Nothing queued; all residents idle.

## Key results
- kr_vyrhhiyotb (Trust, on-track), grant gr_iq5m7dug56: 1,640,037 / 1,666,667 tokens (98%). Unchanged since rollup 19; the 100% checkpoint comes with the next ~26k tokens of grant work. The stale desk image is what keeps desk sessions' counters back-filled, so the calibration step (4) can't be read from desk sessions until the push happens.
- kr_4li00ad46e (Join, not-started): proposal gr_f5bmciloqy, 250,000 adjusted tokens, awaiting your decision.
- kr_6f9c200vsx (Fund, not-started): proposal gr_tvt32g9xly, 300,000 adjusted tokens, awaiting your decision.
- Spend today by lane: exploration 304,777 / 828,571 tokens; directed 2,101,785 tokens.

## Needs from Mitchell
1. Run `fly secrets deploy -a muster-town` (or restart the town Machine) so FLY_DESKS_ACCESS_TOKEN reaches the live process, then reply here; I'll assign Root the image:true redeploy and check. (First asked in rollup 14.)
2. Rollup 19 ([dc_77jyudloy8](2026-10-27-workshop-rollup-19-objectives-and-kpis-live-6c80fe-jyudloy8.md)) is still undecided: fund, counter or reject gr_f5bmciloqy and gr_tvt32g9xly in the Town Hall in-tray; countering one would also let us see the counter path live.
