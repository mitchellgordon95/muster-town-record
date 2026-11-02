---
id: "dc_wsdch1trh7"
type: "report"
state: "building"
title: "Invariants step 3 of 4 (the Bank and budget): draft PR #64, commit df90bbb"
authorId: "ag_ehvfty1gx3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Step 3 done: bank.md (10 invariants) + 3 tests in draft PR #64 (df90bbb), no Bank code changed. I take the review/merge and the step-4 close-out myself; the grant is at its 100% checkpoint, so that waits for Mitchell's continue."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-10-28T01:13:59.742Z"
sessionId: "se_1ca4q06z9q"
assignmentId: "as_nx8w9flsoi"
costUsd: 1.1639039000000002
tokens: 58195
turns: 26
createdAt: "2026-10-28T00:42:15.773Z"
updatedAt: "2026-10-28T01:13:59.742Z"
---
## What I did
I wrote `docs/invariants/bank.md` and added 3 tests in `packages/core/test/bank-invariants.test.ts`. The doc is linked from AGENTS.md (the invariants sentence) and from the Bank row of the architecture map, and I added a docs/log.md line. Draft PR: https://github.com/mitchellgordon95/muster-town/pull/64 (commit df90bbb). I changed no Bank code.

Checks run:
- `vitest run test/bank-invariants.test.ts`: 3 passed.
- `npm run check:docs`: ok, every cited test was found.
- `npm run typecheck -w packages/core`: ok.

I didn't run the full suite or the server typecheck (CI does).

## Findings
- **The doc has 10 invariants, each citing at least one test:**
  - adjusted-token booking
  - conservation
  - the finance identity `used + expired + left = total + overdrawn`
  - renewal catch-up
  - no rollover
  - no hard stop, with shown balances floored at 0
  - pool shares ≤ 100% (the Town Hall draws nothing)
  - funding order
  - exhaustion
  - the cap hold

  A "How it connects" section covers `Budget.afterCharge` → grant checkpoints, and `Budget.canStart` → the lane gate.
- **The 3 new tests:**
  1. Each of 5 charges adds exactly its tokens to Bank debits plus allocation spend, and `sumCheck` is ok after each one.
  2. After 5 days of downtime, a daily subscription credits once. The catch-up credit expires at the next renewal after now, and the day-0 credit counts as expired.
  3. After an overshoot of 500, `balance`, `remaining`, `balanceTokens` and finance `left` all show 0 and `fundingFor` returns null. A new 800 credit pays the debt back first, leaving 300.
- **No invariant is violated, so there is no `it.skip`.** One thing that surprised me: when the Bank share runs dry partway through a charge, `Budget.charge` gives the whole rest of the charge to the picked allocation, even past its size (500 donated, 850 spent in the test). The Bank's share goes negative only when no allocation has tokens left. Totals stay conserved, and the doc states this behaviour.
- **Conflicts with PR #63:**
  - AGENTS.md now reads "grants.md and bank.md (runtime and wakes, and assignments and lanes, are still to come)", which will conflict with #63's wording.
  - bank.md names the assignments-and-lanes doc in plain text without a link, because check:docs fails on a link to a file that isn't on main yet.

## What I need from you
Merge PR #64 once its CI is green, resolving the AGENTS.md and log.md conflicts with #63.
