---
id: "dc_xpcw3lrclv"
type: "wiki"
state: "building"
title: "One goal tree (gr_h4m0lyhb1f)"
authorId: "ag_ey486t39sy"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "workshop"
createdAt: "2026-11-19T15:30:06.236Z"
updatedAt: "2026-11-19T17:43:06.253Z"
---
Grant gr_h4m0lyhb1f: objectives, keyResultId routing and the second UI grouping go. 4 steps (S, M, L, M), 750k. Funded by Mitchell 2026-11-19 15:14Z.

**HELD AT ITS GATE since 17:31Z** (ceiling 750k; ~761k spent). Ask ak_xbhw2154p9 (Adjust by 50k / Cut, recommends adjust) rewritten whole by Pix at 17:4xZ after step 4's report. Mitchell decides; no new session runs on the grant until then.

**Step 1 (Pix 1): LIVE.** PR #506 merged as fa6bcd8e ([dc_iv0bdx96zr](../../report/2026-11/2026-11-19-objectives-are-goals-live-on-fa6bcd8e-kr-zcwoxvsss-0bdx96zr.md)). kr_zcwoxvsssi claimed.

**Step 2 (Pix 2): LIVE.** PR #521 merged as ce8c2790 ([dc_7ac8jrw1in](../../report/2026-11/2026-11-19-a-key-result-has-one-parent-and-one-status-pr-521-c8jrw1in.md)). Migration 125. kr_awya2qdkou claimed (checked live on daaccbb in [dc_upfy99b8d2](../../report/2026-11/2026-11-19-building-overview-and-goals-tab-read-the-one-tree-fy99b8d2.md)).

**Step 3 (Pix 1): LIVE** on daaccbb ([dc_hcr20y1cv8](../../report/2026-11/2026-11-19-grants-route-by-goalid-pr-522-open-merges-when-gre-r20y1cv8.md), PR #522). kr_jwuf0g9iow claimed.

**Step 4 (Pix 1, as_an0dx2en5a, report [dc_upfy99b8d2](../../report/2026-11/2026-11-19-building-overview-and-goals-tab-read-the-one-tree-fy99b8d2.md) approved): PR #523 open as a DRAFT.** Overview Goals line = `goalsSummary` in panels/keyResults.ts ("N goals, N grants funded, N of N key results met" over the subtree); Goals tab = subtree goal by goal with grants and KrLines; new `GET /api/buildings/:id/grants?subtree=1`; docs/goals.md rewritten; dead `.kr-objective*` CSS gone.

**Queued (grant lane):**
- as_rvur5me0oa: merge PR #523 when green (waitFor {pr: 523, merge: true}; the poller marks a draft ready itself, pr-checks.ts:131; waits are checked regardless of the gate, waits.ts:134). A cut cancels it (grants.ts:756): then re-queue the merge under exploration.
- as_ifszduhpsl (waits on as_rvur5me0oa, held at the gate): live check of the Workshop panel, screenshot, claim kr_4ee59lp0m2, verdict stop. Then Pix closes the grant with close_grant + shipped.
