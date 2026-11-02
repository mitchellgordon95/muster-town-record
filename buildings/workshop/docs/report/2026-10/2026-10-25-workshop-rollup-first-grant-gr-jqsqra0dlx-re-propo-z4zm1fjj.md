---
id: "dc_ucz4zm1fjj"
type: "report"
state: "building"
title: "Workshop rollup: first grant gr_jqsqra0dlx re-proposed at Mitchell's counter (24M tokens); KR1–3 work queued and held until it is funded"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_ht1mmyink1","dc_rv3zopioqh","dc_gac5p4math","dc_hm1nc83na4","dc_cqismr9ynx","dc_wy7tz61d69"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-25T18:51:07.739Z"
sessionId: "se_xj9t8jkdks"
createdAt: "2026-10-25T16:59:42.756Z"
updatedAt: "2026-10-25T18:51:07.739Z"
---
## Shipped
- **db92a88** (Lena): grant token inputs in millions. Fund/Counter/Adjust and exploration-per-day take M tokens; whole millions print without ".0". Live on muster.town; the Town Hall in-tray shows "asks 24M tokens" ([dc_cqismr9ynx](2026-10-25-db92a88-is-live-the-in-tray-shows-amounts-in-milli-ismr9ynx.md)). The Fund/Counter form gets its live check when you open the re-proposed grant.
- **0059285** (Keel): Budget mode control in Building → Settings, human-only. Live; the Workshop has been goal-directed since 10-25 ([dc_ht1mmyink1](2026-10-25-0059285-is-live-but-the-workshop-is-still-budgetmo-1mmyink1.md), [dc_rv3zopioqh](2026-10-25-workshop-is-still-budgetmode-open-at-08-00-utc-par-3zopioqh.md) were the re-checks before the flip).
- **gr_jqsqra0dlx**: proposed 16:41Z at 275M tokens ([dc_gac5p4math](2026-10-25-workshop-s-first-grant-proposed-gr-jqsqra0dlx-275m-c5p4math.md)) → you countered to 24M at 16:44Z → re-proposed at 24M, same id, 16:58Z ([dc_wy7tz61d69](2026-10-25-gr-jqsqra0dlx-re-proposed-at-mitchell-s-counter-24-7tz61d69.md)). Status `proposed` in the Town Hall in-tray. No code change for the re-proposal.

## Decided
- [dc_ht1mmyink1](2026-10-25-0059285-is-live-but-the-workshop-is-still-budgetmo-1mmyink1.md), [dc_rv3zopioqh](2026-10-25-workshop-is-still-budgetmode-open-at-08-00-utc-par-3zopioqh.md) (Keel, parked 7a re-checks): approve; the flip happened, his continuation closed.
- [dc_gac5p4math](2026-10-25-workshop-s-first-grant-proposed-gr-jqsqra0dlx-275m-c5p4math.md) (Pix, first proposal at 275M): approve; superseded by your counter.
- [dc_hm1nc83na4](2026-10-25-grant-token-inputs-in-millions-pushed-to-main-db92-1nc83na4.md) (Lena, millions inputs): approve; live check followed.
- [dc_cqismr9ynx](2026-10-25-db92a88-is-live-the-in-tray-shows-amounts-in-milli-ismr9ynx.md) (Lena, live check of db92a88): approve; done.
- [dc_wy7tz61d69](2026-10-25-gr-jqsqra0dlx-re-proposed-at-mitchell-s-counter-24-7tz61d69.md) (Pix, re-proposal at 24M): approve; done, escalated here.

## Key results
No funded grant yet. gr_jqsqra0dlx (24M tokens, checkpoints at 12M and 24M) is `proposed`:
- KR1 autonomous work (kr_zrjhc51fc4): Keel as_1znskqwqoh, held "grant not funded yet".
- KR2 single explicit blocker + unblock (kr_a3qo30oe5b): Lena as_gyi0qt04yo, held.
- KR3 fund/checkpoint/new-KR wakes the manager (kr_tezc1nboh6): Root as_gz2yaa0s7u, held. Kelly's audit ([dc_362tfcb7qi](../../../../bl_hzjw0z0zlz/docs/note/2026-10/2026-10-25-what-wakes-a-manager-today-and-the-smallest-change-2tfcb7qi.md)) scopes it to a ~25-line fix in the grant decide path.
All three start by themselves the moment the grant is funded. Exploration spend today: 1.88M of 4M tokens.

## Needs from Mitchell
1. Fund gr_jqsqra0dlx (24M tokens) in the Town Hall in-tray. Nothing else.
