---
id: "dc_ipcpcdwqog"
type: "report"
state: "building"
title: "Dead exports are growing again (149 → 207 in 3 days, dead web `Feed`): new KR kr_ealc55cjf5, proposed gr_83jxsu8u0o (70k) to add knip's exports check to check:deadcode"
authorId: "ag_kdvqxn0lk7"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_qortjdoqsd","dc_vwlbhi4lx0","dc_2ntbv19gwt"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Clean exploration: findings filed (dc_qortjdoqsd), KR kr_ealc55cjf5 written, proposal gr_83jxsu8u0o open with Mitchell. Nothing to run until he decides the grant."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-10-31T20:26:41.051Z"
sessionId: "se_uyx9bb2elp"
assignmentId: "as_43cvji17fx"
costUsd: 0.8239187
tokens: 41196
turns: 23
createdAt: "2026-10-31T20:25:19.264Z"
updatedAt: "2026-10-31T20:26:41.051Z"
---
## What I did
I ran knip with exports and types at main 9fe1873 and compared the result with Finn's 10-28 sweep ([dc_vwlbhi4lx0](2026-10-28-dead-code-sweep-1-14-candidates-and-a-code-level-f-lbhi4lx0.md)). I classified each hit with git grep and timed the check. Findings are filed in [dc_qortjdoqsd](../../note/2026-10/2026-10-31-dead-exports-are-back-knip-s-deferred-exports-chec-rtjdoqsd.md). I wrote key result kr_ealc55cjf5 on the building goal, proposed grant gr_83jxsu8u0o (70k, one PR) and rewrote the topic page "Dead-code sweeps" ([dc_2ntbv19gwt](../../wiki/2026-10/2026-10-29-dead-code-sweeps-tbv19gwt.md)). No code changed.

## Findings
- `check:deadcode` still checks only files and dependencies. Finn's recipe deferred the exports check "after a ~20k cleanup", and that step never shipped.
- Unused exports are now 141 plus 66 types (207 in total), up from 94 plus 55 (149) on 10-28: +58 in three days.
- 118 of the 141 exports are only used inside their own file, so only the `export` keyword is extra.
- Two are dead functions:
  - `Feed` in web panels/ui.tsx:136, dead since c9f7338 today.
  - `placeAt` in web state.ts:302.
- `EVENT_TONE` is copied in both ui.tsx and AgentPanel.tsx.
- Adding exports and types costs about 0.3 s (6.3 s vs 6.0 s, one run each on 1 CPU).
- The grant runs `knip --fix`, checks the name-shared hits by hand, deletes the dead bodies and adds exports and types to `check:deadcode`. The stop condition is CI green on main. Its note flags that the keyword removals touch other buildings' files.

## What I need from you
Nothing needed.
