---
id: "dc_erdzbzyu9g"
type: "report"
state: "building"
title: "Goal tree step 6 merged (PR #130, 18f96f4): postmortems on missed KRs + read-only Queue tabs; live check parked"
authorId: "ag_e0acy7cyid"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["mt_kh0zaqui0w","dc_0xqyrevla1"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/130"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. Step 6 (PR #130, 18f96f4: postmortems on missed KRs + read-only Queue tabs; no migration, no Bank code) is merged and the redeploy is queued; the live check as_7ceg02tdxb resumes on the deploy by itself. Shipped item for rollup 34 once the live check is in. Steps 7-8 stay gated on Mitchell's Bank yes (rollup 33 Needs)."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T00:49:33.805Z"
sessionId: "se_cd09xk9cjk"
assignmentId: "as_i7tay9shzl"
costUsd: 3.3801899000000013
tokens: 169009
turns: 66
createdAt: "2026-10-31T00:49:24.629Z"
updatedAt: "2026-10-31T00:49:33.805Z"
---
## What I did
Built goal tree step 6 from docs/goals.md: postmortems on missed key results, and a read-only kanban (Queue tabs). Merged it as PR #130 (https://github.com/mitchellgordon95/muster-town/pull/130), merge commit **18f96f4** on main. I had to merge main into the branch twice because Nell's PRs #129 and #131 landed during the session. The only conflict was in docs/log.md. `npm run check` passed after each merge (docs, dead code, typecheck, all tests). I queued a redeploy, so **18f96f4 should be live** after it. The live check is parked on that deploy. I rewrote topic page [dc_0xqyrevla1](../../wiki/2026-10/2026-10-30-town-level-goal-tree-design-qyrevla1.md).

## Findings
- **Postmortems** (core `postmortems.ts`):
  - A human who marks a key result missed must now give a reason. Without one the server answers 400 "Say why it was missed".
  - The reason is filed as the human's own note, tagged `postmortem-of:kr_…`. It goes to the building whose latest grant named the key result, or to the building that proposed it if no grant did.
  - That note queues one directed building-queue assignment, "Postmortem on kr_…", with the note as its source. The tagged note stops a second postmortem for the same key result.
  - Archiving a key result as missed in a reorg goes the same way.
  - When the postmortem's final (not parked) report is filed, it is set as the key result's `postmortemDocId` and tagged `postmortem`. The key result's `updatedAt` stays the date it was marked missed, so the Spend tab's results window doesn't move.
  - Web: Missed and Archive open a "why" form in the goal editor. The building Goals tab asks in a prompt. Missed key results show a "postmortem" link, or "postmortem pending" until the report is in.
- **Kanban** (core `kanban.ts`):
  - New routes `GET /api/buildings/:id/queue` and `GET /api/goals/:id/queue`. The goal route gives one swimlane per building attached anywhere under the goal.
  - Columns: Queued; Held (with the held reason, an unmet wait, or "offered to a visitor"); Running (with the live session's adjusted tokens, header "n / headcount desks"); Done (done or cancelled in the last 24 h, linking the report).
  - It is a public, read-only view over assignments: no reordering and nothing new enforced.
  - Web: a "Queue" tab on the building panel (before Schedule) and on a goal's detail in the Goal tree.
- **Tests:** new core/test/goals-step6.test.ts with 3 tests: why required, one postmortem per key result, report linked back, reorg archive, nothing for met, all four columns, the 24 h drop-off and the subtree roll-up. The web tab-list test now includes Queue.
- **No migration** (`postmortemDocId` came with 061) and **no Bank or token-accounting code**. The kanban only reads `adjustedOfUsage` to show live tokens; bank.ts is untouched.
- **Left out:** a key result proposed at the end of a postmortem gets no special handling. It goes through `propose_key_result` like any other.

## What I need from you
Nothing needed.
