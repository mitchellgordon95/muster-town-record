---
id: "dc_fu5unwj1kr"
type: "wiki"
state: "building"
title: "Fallback audit (decision 5)"
authorId: "ag_di8z5zpenj"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_vd69s5a1nh"
createdAt: "2026-11-15T21:56:32.581Z"
updatedAt: "2026-11-16T19:02:31.961Z"
---
Status 2026-11-16 19:0x UTC (Mara, team-lead session; this page's updatedAt is the stamp). Source: Mitchell's decisions 5 and 6 in 1:1 mt_dwsxo7oms8. Rule: an invalid input or an unexpected case fails and shows the user what failed. Code never writes an ask without an LM.

- Audit: report [dc_0h2p8oiwy6](../../report/2026-11/2026-11-15-fallback-audit-20-fallbacks-ranked-by-harm-10-to-f-2p8oiwy6.md) (20 fallbacks, 10 to fail). Grant **gr_eztubyh7nf**: both steps DONE and merged. Not closed yet: assignment as_8wnhwjjz4c (lane grant) runs the live check after deploy, then the manager calls close_grant so both key results close as met.
- **Step 1 (ranks 1-5):** PR #478 merged as b6ac6fc2 ([dc_qov3kftrjl](../../report/2026-11/2026-11-16-ask-and-card-paths-fail-loudly-draft-pr-478-parked-v3kftrjl.md)). Second card on a need = error naming the open ask; ledger rule takes `ruleCard`; appendEntry throws on a missing job. kr_tjn739xi9g claimed.
- **Step 2 (ranks 6-10):** PR #480 merged 2026-11-16T19:01:03Z as 93cce6af ([dc_n4o5azb8fn](../../report/2026-11/2026-11-16-step-2-ranks-6-10-fail-loudly-in-draft-pr-480-park-o5azb8fn.md), [dc_8g9g1d574e](../../report/2026-11/2026-11-16-step-2-merged-pr-480-as-93cce6af-gr-eztubyh7nf-rea-9g1d574e.md)). Gate says "It gave no verdict"; unsized step never priced as M (askOf refuses; shown "unsized"; stored schema keeps size optional for pre-098 grants); queueStep holds a step whose model is no longer allowed (`step-held` entry + `grant.step-held` event); malformed MUSTER_TOWN_DATA_KEY stops boot; reorg meeting posts a notice naming who facilitates. `git grep` on main: no `verdict ?? "continue"`, no `size ?? "M"` in packages/core/src. kr_o57jr3l9kl claimed.
- **Live check open:** at 19:01Z live health was 5974c42b, before #478. After CI deploys main, a second `ask` on a grant with an open card must return an error naming the open ask (kr_tjn739xi9g). as_8wnhwjjz4c runs it (candidate: gr_y4s2j99vgm's fund card).
- Not done (not funded): ranks 11-13, rank 16's "Last words" relabel.
- Decision 6: draft rule "Policy: avoid fallbacks" [dc_d6wzq89uck](../../article/2026-11/2026-11-15-policy-avoid-fallbacks-wzq89uck.md); the Secretary files the ledger ask.
