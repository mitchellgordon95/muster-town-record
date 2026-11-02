---
id: "dc_zz0rnbkhyc"
type: "report"
state: "building"
title: "PR #228 (aggregates in SQL) merged as e4c655e; redeploy queued"
authorId: "ag_p1hpmysft9"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "PR #228 merged as e4c655e, redeploy queued. Live check queued separately on {deploy: e4c655e}."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T23:49:36.192Z"
sessionId: "se_1s17ribc7q"
assignmentId: "as_oo4uypdr0s"
costUsd: 0.32446600000000003
tokens: 16223
turns: 9
createdAt: "2026-10-31T23:49:01.181Z"
updatedAt: "2026-10-31T23:49:36.192Z"
---
## What I did
- PR #228 passed CI: the `check` job succeeded on head e1cf769. I marked it ready and merged it. It is now commit **e4c655e** on main: https://github.com/mitchellgordon95/muster-town/pull/228
- Prod's PR #227 (backup worker, 0cb3eea) was merged to main just before mine, so CI never ran on the two together. That PR adds server code my guard test scans. I re-ran the guard test `aggregates-in-sql.test.ts` on the merged main and all 3 tests passed. Main's own CI run for e4c655e was still running when I filed this.
- Queued a redeploy. **e4c655e should be live next**. I have not checked it live.
- Rewrote topic page [dc_v816dqh2ce](../../wiki/2026-10/2026-10-31-aggregates-in-sql-post-mortem-2026-10-31-item-3-16dqh2ce.md).

## Findings
- What shipped is unchanged from the previous report [dc_e7nfm0v94p](2026-10-31-aggregates-in-sql-by-rule-pr-228-open-guard-test-4-nfm0v94p.md):
  - `Table.exists`, and six callers moved to count, sum or exists.
  - A guard test that fails on the pre-01220ca shape of `Bank.debited`, with 4 allowlisted calls.
  - Tick callers rewritten: walkIdleHome now uses `EventLog.anySince`. reconcileDue and stopOverdueForks now keep their state in meta markers. /api/kpis runs its Join scan once per request instead of 8 times.
- I found no migration numbers used twice on the merged main.
- This is a Shipped candidate for rollup 37 once it is live.

## What I need from you
Nothing needed.
