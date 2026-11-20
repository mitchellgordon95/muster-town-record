---
id: "dc_nllgamgxvb"
type: "report"
state: "building"
title: "Proposed gr_6id9g7u9cj: the explore tick backs off after empty explorations (Onboarding looped 29× on 11-19)"
authorId: "ag_8g99fu6lpl"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Read the report, the findings (dc_ak5bbb6iyd) and explore.ts: the 30-min-only spacing (EXPLORE_MIN_GAP_MS, explore.ts:23/51) and the cap check (explore.ts:57, free-tokens.ts:218) match the analysis. gr_6id9g7u9cj is proposed with its ask card; Mitchell decides it in the Town Hall in-tray, nothing more to file. The 5.6% first-run figure goes into gr_baf19xtg7p's close after sc_w67mqora3r's second window (11-25)."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-20T00:04:05.765Z"
sessionId: "se_khinb7ggnp"
assignmentId: "as_az15d5xn1a"
costUsd: 1.2434456000000003
tokens: 62172
turns: 26
createdAt: "2026-11-20T00:03:08.934Z"
updatedAt: "2026-11-20T00:04:05.765Z"
---
## What I did
I read the last 200 sessions (/api/sessions, 11-17 03:52Z to 11-20 00:00Z) with their assignment titles and exploration reports. I also checked PR first-run CI since PR #499. Then I read packages/core/src/explore.ts and free-tokens.ts. I filed findings [dc_ak5bbb6iyd](../../note/2026-11/2026-11-20-findings-the-explore-tick-re-runs-an-empty-explora-5bbb6iyd.md) and proposed gr_6id9g7u9cj (200k: M, S) with its ask card.

## Findings
- On 2026-11-19, Onboarding ran **29 empty explorations**, one every 30 min from 00:30Z to 14:30Z. Each was 5 turns and 9.5k–11.7k adjusted tokens, **306,070 in total**. Example reports: [dc_ic7y7ns84a](../../../../bl_hzjw0z0zlz/docs/report/2026-11/2026-11-19-explore-no-new-grant-nothing-moved-under-this-goal-7y7ns84a.md), [dc_sovbjif48w](../../../../bl_hzjw0z0zlz/docs/report/2026-11/2026-11-19-explore-no-new-grant-nothing-moved-under-this-goal-vbjif48w.md). Its manager has no switch to stop them. Other buildings had only 4 empty explorations in those 3 days, all follow-ups closing real work.
- Cause: `exploreBlock` (packages/core/src/explore.ts) spaces explorers only by EXPLORE_MIN_GAP_MS = 30 min. Nothing records an empty outcome. Spend from the loop counts toward the 500,000/day town cap (`exploreSpentToday`, free-tokens.ts:218). From the arithmetic, I infer the loop used the cap up and blocked other buildings after 14:30Z. I have not checked this against the tick events. Step 1 checks it.
- The proposal: each empty exploration doubles the gap, up to 24 h. A proposal, queued work, or a human decision or message resets it. The Queue tab shows the wait. Step 2 measures 7 days live. KRs: kr_o83giwqnc1 (due 11-24) and kr_dcttivwo6c (no building has more than 6 empty explorations a day, under 100k tokens a day town-wide, due 12-02).
- Side check: for gr_baf19xtg7p kr_o6jibyr7jj, 2 of 36 PR first runs failed (5.6%) after PR #499 (2026-11-17 22:09Z). One was an image build and one a real test failure. That is under the 6% target. The grant's close report can use this figure.

## What I need from you
Decide on gr_6id9g7u9cj (fund, counter or reject) in the Town Hall in-tray.
