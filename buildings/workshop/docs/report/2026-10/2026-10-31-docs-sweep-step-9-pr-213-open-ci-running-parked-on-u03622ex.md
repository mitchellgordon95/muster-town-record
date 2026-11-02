---
id: "dc_19u03622ex"
type: "report"
state: "building"
title: "Docs sweep (step 9): PR #213 open, CI running; parked on {pr:213}"
authorId: "ag_av52tsu1wz"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Docs sweep PR #213 open; your parked continuation (as_jbq2k9ha2r on {pr: 213}) merges it if green, redeploys and rewrites the three topic pages. The leftovers you listed (\"pool\" test names, caps.ts comment, GrantBoard.keyResults, goals.md unmarked sections) stay as notes, not new work, unless Mitchell asks."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T22:04:45.510Z"
sessionId: "se_nyg6w41iqe"
assignmentId: "as_3bzb2g8si6"
costUsd: 1.9618056000000001
tokens: 98090
turns: 44
createdAt: "2026-10-31T22:02:07.405Z"
updatedAt: "2026-10-31T22:04:45.510Z"
---
## What I did
- `git fetch`: all three build steps are on main: #169 = 8d18dbc, #173 = 49afcdd, #171 = 5bead7f.
- Opened one docs PR, **https://github.com/mitchellgordon95/muster-town/pull/213** (draft). It also changes two code strings. Locally: check:docs ok, typecheck ok, core tests touched green (finance-fly, finance-spend, grants, free-tokens, explore), web finance + manual green.
- Merged main in at b295b39. That brings #209's fix for the finance-fly test, which was red on main because of 48a7d53.

## Findings
- Files touched:
  - `docs/architecture.md`: added the explore tick (a node in the work-flow diagram, plus an Exploration bullet that replaces the allowance one), the `bank_reservations` row, grants with `goalId` and their key results, `goal_captain_requests`, and the draw order through `Budget.fundingFor`. Dropped `propose_key_result`.
  - `AGENTS.md`: one sentence on how work is steered (grants carry key results, the tick explores on a reserved chunk).
  - `docs/invariants/bank.md`:
    - New 7b: a reservation claims its chunk until it closes. Named by two explore.test.ts tests.
    - Invariant 8 now has the earmark in the funding order, with the streams.test.ts test.
    - The "How it connects" section no longer mentions an allowance, and its cap hold reference now points to invariant 12.
  - `docs/invariants/grants.md`: the design pointer goes to §4, and "exploration names a gap, never a key result".
  - `docs/invariants/assignments-lanes.md`: already true to the code (no change).
  - `docs/goals.md`, `goal-directed-budgets.md`, `waterfall.md`: 5 superseded sections cut to their pointer line. goals.md "Who can change the tree" keeps one line saying what is true today.
  - `docs/bank.md`: the streams section was still current, so I kept it. I removed its superseded marker, fixed `nodeOf` (it reads the grant's goalId first), and added reservations.
  - `docs/how-work-gets-done.md`: §10 has a "Landed" note. §11 Status lists every step's PR sha; steps 7 and 8 are marked built (#168; #179 as a picker); the step 2 text no longer says forks may call `set_key_result`. §12 q3 is answered (a town-wide picker, 1:1 mt_q10xf3bkoq). I found no answers to q1, q2, q4 or q5.
  - `docs/manual.md`: the stoplight is "grey" (that is what the code says), an explorer's proposal shows "in the Town Hall in-tray", and admins and captains pick "the map's" Shape. It is at 1874/1900 words.
  - `docs/log.md`: one line.
  - Code, strings only:
    - `packages/core/src/grants.ts`: "Only a human … a grant's key result."
    - `packages/core/src/finance-spend.ts` NO_GRANT, plus its web test: "work a building took up on its own" replaces "the building's own daily allowance". The spend section must not name lanes, and the test enforces that.
- What the code still has that no doc covers, or that still uses the old words:
  - Test names still say "pool": finance.test, bank-invariants.test, member-funding.test, running-debit.test. They are cited verbatim in docs/invariants/bank.md, so renaming them is a separate change.
  - `caps.ts` comment and `budget.exhausted` still mention an agent's "daily allowance".
  - `GrantBoard.keyResults` and `blocked` are still on the grants board type.
  - goals.md's unmarked sections (the goal editor's "+ Key result", Data model) still describe goal key results. The doc only asked to cut the sections marked superseded.
- Plan on resume: if CI is green, mark #213 ready and merge it. Redeploy, because the strings changed, and say the merge sha should be live. Then rewrite the topic pages [dc_rke20gvrqr](../../wiki/2026-10/2026-10-28-bank-and-token-accounting-e20gvrqr.md), [dc_oghes5lgud](../../wiki/2026-10/2026-10-28-grants-key-results-and-the-town-hall-in-tray-hes5lgud.md) and [dc_4su2e5yyhn](../../wiki/2026-10/2026-10-31-how-work-gets-done-vision-doc-u2e5yyhn.md), and file verdict stop.

## What I need from you
Nothing needed.
