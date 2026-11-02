---
id: "dc_32p3strium"
type: "report"
state: "building"
title: "gr_glon8xr0io (remove `open` budget mode) cut into 3 steps; step 1 (core + schema + tests) queued to Finn behind his dead-code step 2"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_vie3wrhj54","dc_fpui0p5b1y","dc_ua7u4b5nj9"],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decisionNote: "Steps 1–3 of gr_glon8xr0io are already queued (as_pg5q3cgkda behind as_w48xxf79jl); nothing further to assign until step 1 reports."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-10-28T19:23:24.937Z"
sessionId: "se_zulrst9rwj"
assignmentId: "as_tqbel9k403"
costUsd: 1.50992155
tokens: 30198
turns: 15
createdAt: "2026-10-28T19:23:06.686Z"
updatedAt: "2026-10-28T19:23:24.937Z"
---
## What I did
- Read the grant plan, Nell's flag inventory [dc_vie3wrhj54](../../../../bl_vef3v0oux0/docs/note/2026-10/2026-10-28-per-building-flags-where-each-is-set-who-flips-it-e3wrhj54.md) and re-grepped the sites at main 869f76d (unchanged from the proposal: lanes.ts:11, grants.ts 4 sites, prompts.ts 2, entities.ts:41, ops.ts:57-59, schema :211/:1331, routes/grants.ts:96; web BuildingPanel/Places/keyResults/mock; 17 test files).
- Cut the plan into three sessions, one owner and one PR for the code:
  1. **Core + schema + tests** (Finn, as_pg5q3cgkda, lane grant): the lane gate becomes `kind !== "town-hall"`, every other reader excludes the Town Hall by kind, the PATCH stops accepting budgetMode, the 17 test files lose their `open` cases, plus a lanes.test.ts regression (lab without budgetMode is gated, Town Hall not). Draft PR, CI green on attempt 1. Check: `grep -rn budgetMode packages/*/src` shows only the schema column and the web sites step 2 removes. ~100k.
  2. **Web + docs** (Finn, same branch, assigned when step 1 reports): Settings select and empty-state text go, board/stoplight/mock go by kind; the 7 docs stop describing a choice; check:docs green; PR ready. ~60k.
  3. **Merge, redeploy, verify, close** (me): PR and main CI attempt-1 green, redeploy, muster.town Settings shows no Budget mode, /api/health budgets lists the five labs and no Town Hall, Town Hall has no stoplight; then close_grant with that evidence and a rollup.
- Step 1 waits for Finn's running exploration as_w48xxf79jl (dead-code step 2) so one person touches core at a time and the knip check lands first.
- Approved the Town notice [dc_ua7u4b5nj9](2026-10-28-key-result-kr-dctpbbwtno-marked-met-by-mitchell-7u4b5nj9.md) (Mitchell marked kr_dctpbbwtno met).

## Findings
- Nothing on main changed this session; live code is 869f76d.
- The `budgetMode` column stays in the schema and the DB, unread; dropping it is a later migration and Mitchell's call. Step 1 will report if anything (seed, import, cli) still writes `open`.
- No rollup due: the last one was at 18:30Z and funding is not an escalation. The next rollup goes out when Finn's step 2 or the grant's step 1 lands.

## What I need from you
Nothing needed.
