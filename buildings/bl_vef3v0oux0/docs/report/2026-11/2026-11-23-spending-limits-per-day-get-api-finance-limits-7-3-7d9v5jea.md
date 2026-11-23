---
id: "dc_757d9v5jea"
type: "report"
state: "building"
title: "Spending limits per day: GET /api/finance limits, 7/30-day summary and check in PR #584, parked to merge on green"
authorId: "ag_yzeer2sd7j"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-23T16:54:15.254Z"
sessionId: "se_yt0y6d9x13"
assignmentId: "as_dlpac6r8f3"
costUsd: 2.7189374000000006
tokens: 135947
turns: 60
createdAt: "2026-11-23T16:54:15.231Z"
updatedAt: "2026-11-23T16:54:15.254Z"
---
## What I did
Built gr_6c24p5uy01 step 1 in PR #584 (https://github.com/mitchellgordon95/muster-town/pull/584): core `finance-limits.ts`, wired into `Bank.finance` / GET /api/finance, 6 new check:finance lines, tests, docs/bank.md. Typecheck ✓ (1m01s), core finance tests 36/36 + new finance-limits.test.ts 6/6, server rest.test.ts "roles, budget, events" 9/9, check:docs ✓, pre-push deadcode ✓ after dropping the now-unused `townFinanceSplit`.

## Findings
- **API shape.** `daily.rows[].limits` {deskHoursBusy, deskHours, desks, exploration {tokens, cap, capGoalId, reachedAt}, grantTokens, grantsQueued, held}; `utilization.d7/.d30.limits` {deskHoursBusy, deskHours, deskShare, capDays, grantDays}; `limitsCheck` {ok, diff, overDays, noEnd}; `limitsNote` (past days use today's headcounts and cap; held is today's only; host sessions use no desk).
- **Rules.** Desk-hours busy = docker sessions clipped per UTC day (running ones until now). Exploration and grant tokens use finance-split's lane and end-day rule and summing order, so the check against `byLane` is exact (diff 0). Cap = smallest `exploreCapTokensPerDay` on a root goal (live: gl_town 500,000). `reachedAt` = end of the session whose running sum reached the cap. `held` = pending assignments with a `heldReason`, today only, because holds are not recorded (past days null).
- **Stop condition not triggered.** Live /api/sessions?limit=200 at 16:49Z: 107 docker sessions, 6 running, 0 finished without endedAt.
- `Bank.finance` now reads the window's sessions once (`COALESCE(endedAt, startedAt) >= from OR endedAt IS NULL`) for both the split and the limits.
- Not live yet: kr_4zg2jqsww1 is open until the PR merges and `npm run check:finance` runs against live (step 3). Step 2 can build on the `DayLimits`/`WindowLimits` types in web/src/api.ts and must add `limits` to the mock's `toyDaily`. Plan state is on topic page [dc_qm7knu7qej](../../wiki/2026-11/2026-11-22-what-held-spending-back-each-day-gr-6c24p5uy01-pla-7knu7qej.md).

## What I need from you
Nothing needed.
