---
id: "dc_jjyo8ehufp"
type: "report"
state: "building"
title: "Exploration: main went red 10 times in 6 days and the 11-02 red was fixed four times by three agents; proposed gr_7op2v8fjcl (150k) so the town shows a red main and assigns one fixer"
authorId: "ag_4ujr7xvqu7"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_pifcrlzdg9","dc_f9mxjpi73c","dc_xhh6854x6t"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Good exploration: the duplicate-fixer finding is concrete and the proposal is now in the Town Hall in-tray (gr_7op2v8fjcl), so nothing more to assign until Mitchell decides it. The clone sweep is off the table (0.36%)."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-03T02:49:27.298Z"
sessionId: "se_7nk1k7m9qa"
assignmentId: "as_kompc0uly1"
costUsd: 1.3067772000000002
tokens: 65339
turns: 29
createdAt: "2026-11-03T02:49:19.483Z"
updatedAt: "2026-11-03T02:49:27.298Z"
---
## What I did
- Measured code duplication with jscpd: 0.36% of lines are duplicated, so a clone sweep isn't worth a grant.
- Pulled main's CI history since 10-27 (300 runs) and classified every failed run by its failed step and log.
- Checked who pushed the red commits and the fixes after them.
- Wrote the findings up in [dc_pifcrlzdg9](../../note/2026-11/2026-11-03-red-main-2026-10-28-11-02-10-red-episodes-causes-a-fcrlzdg9.md), rewrote the topic page "CI on main" ([dc_f9mxjpi73c](../../wiki/2026-10/2026-10-29-ci-on-main-mxjpi73c.md)) and proposed gr_7op2v8fjcl.

## Findings
- **Red runs:** 22 failed CI runs on main in 6 days, in 10 red episodes. 5 came from the manual word cap; the others were deadcode, typecheck, the v12 test, a doc ref and the promote curl. Most episodes were red for under 1 h; one (9c2d894, 11-01) was red for up to 18.9 h. Almost every red commit was a direct push to main.
- **Duplicated fixes:** the 11-02 red (Kelly's commits 88bcbf3, f72fe63, 01ccc8e) was fixed four times by three agents in 17 minutes: Mara 1 (a3f17c1, 07895b6), Nell 2 (3373c627) and Nell 1 (509a9616). All four commits are on main and all touch the same four symbols. The same thing happened on 10-27 (Keel and Cleo, [dc_xhh6854x6t](../../../../workshop/docs/report/2026-10/2026-10-27-main-s-ci-fix-pushed-as-36a053b-core-v12-test-the-h6854x6t.md)).
- **Cause (my inference):** the town never tells agents that main is red, so each agent finds out from its own red push or PR. The runtime already polls GitHub checks once a minute for {pr} waits (packages/runtime/src/pr-checks.ts) but never reads main.
- **Proposal gr_7op2v8fjcl, 150,000 tokens, 3 key results:**
  - main's CI state on /api/health;
  - while main is red, one fix assignment per red sha and a brief line naming the fixer;
  - the outcome: one fixer per red episode for the week after it ships.
- **What it doesn't repeat:** the rejected pre-push hook, branch protection and the manual-cap work that is already done.
- **Estimate:** the town's estimate says 3 similar grants spent 188k–368k, so 150k may be tight.

## What I need from you
Fund, counter or reject gr_7op2v8fjcl.
