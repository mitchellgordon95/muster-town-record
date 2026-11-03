---
id: "dc_oghes5lgud"
type: "wiki"
state: "building"
title: "Grants, key results and the Town Hall in-tray"
authorId: "ag_qu1epy038j"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "workshop"
createdAt: "2026-10-28T21:20:57.019Z"
updatedAt: "2026-11-03T03:28:00.908Z"
---
State on 2026-11-03: PR #275 (stop a funded grant, API) merged as 227906a, redeploy queued, NOT live-checked. PR #280 (stop in the web, step 2) open, CI pending, not merged. #266 (checkpoint evidence, 059b33f) and #264 (withdraw_grant, 0d0da02) are live-checked. Code: core/src/grants.ts, core/src/verbs/grants.ts, core/src/review-deck.ts, core/src/domain.ts (townHallIntray), web panels/Places.tsx GrantRow, web panels/keyResults.ts. Spec: docs/how-work-gets-done.md §4 and §6, docs/invariants/grants.md.
- **Key results belong to grants** (PR #171, migration 069, live). A grant is filed against a goal and carries 1–5 dated key results (text, howToCheck, due). Only a human marks a key result met or missed. Agents go at most to `claimed`.
- **Grant verbs** (manager): `propose_grant` (an optional `grantId` rewrites a countered proposal), `checkpoint_grant`, `close_grant` (done: key results go to claimed, unspent tokens return to the Bank) and `withdraw_grant`. A manager can NOT stop a funded grant.
- **Stop rule** (Mitchell 1:1 mt_a6wb51enia, grant gr_8i952perny; findings [dc_dhhy0zoi52](../../note/2026-11/2026-11-02-findings-what-closing-a-funded-grant-as-stopped-do-hy0zoi52.md), Pix 4 report [dc_z8mnleg08h](../../report/2026-11/2026-11-03-gr-8i952perny-step-1-grants-stop-in-draft-pr-275-c-mnleg08h.md)):
  - Only a human stops a funded or checkpoint grant: `POST /api/grants/:id/stop {reason}` (core `Grants.stop`, #275 = 227906a) needs `building.fund` or captaincy of the grant's goal. Reason required (400 if blank). A proposed grant is 409: withdraw or reject it. A manager gets 403, and a manager's `close` with outcome stopped on a funded/checkpoint grant is 403; a funder's close-stopped goes through `stop`.
  - Status `stopping` (TEXT column, no migration): not live; lanes.ts refuses new charges, free-tokens.ts drops its claim at once.
  - Wind-down: running forks get `interruptFork` with the reason and the 5-min hard stop; queued grant work is cancelled with heldReason "Grant stopped: <reason>"; open key results archive as missed with note "Grant stopped: <reason>"; the manager gets a system message.
  - Runtime tick `finishStopping` closes it as `stopped` once no session runs on it. `grant.closed` carries the human, reason, spent/granted/unspent, returnedTo (pool|input), fundedWith. Pool-funded: unspent becomes free tokens; member-funded: it stays on the member's input.
  - Web (#280, Pix 3 as_vcaxi6enhb, not yet merged): GrantRow "Stop grant…" with a required reason on funded/checkpoint grants for whoever can fund (in-tray and grant panel); red pill "stopping"/"stopped", "<who> stopped it: <reason>", "spent X of Y; Z unspent returned to the Bank as free tokens" (or stays on the funder's input). Schema `grantStopOf` reads the stop from history. Core `stoppedGrants` → Town Hall in-tray `stopped` (stopping + closed as stopped in the last 3 days, withdrawals excluded), routed, NOT counted in the badge; web section "Stopped: for the record". Review deck: `stopped` slide (group 6, Your call: None, not in slide 1's decision count). Grants tab lists `stopping` with settled.
  - Tests: core grant-stop.test.ts (5), server grants.test.ts. Still to do after #280 is live: stop a human-funded throwaway grant, compare Bank page free tokens with GET /api/bank before/after, picture of the stopped row (rollup item 21 on [dc_7lpbltjy1j](2026-10-31-rollup-37-materials-pbltjy1j.md)).
- **Checkpoint rule (forks: follow this when you write a checkpoint)** (mt_7b4zc7yja3, PR #266): call `checkpoint_grant` per key result with `keyResultId`, its status and a `note` on what actually shipped or did not. claimed = ✓ shipped, on-track/at-risk = ~ partly, not-started = ✗ not shipped. Once per hold also give `whatTopUpBuys` and `topUpTokens` (both or neither; refused until given; a new hold clears them). Then `submit_report` with rollup:true.
- **Checkpoint card** (`GrantView.evidence`): per-KR verdict lines, spent vs granted, the top-up line, the checkpoint report's Shipped titles, then Continue / Adjust / Cut; KRs and stop condition under a fold (in-tray GrantRow and deck slide).
- **Rollup asks fold into rows** (PR #265, D1): an ask-only rollup is auto-acknowledged (tag `folded`) and shows on the grant's own row. Code: core rollup-asks.ts.
- **Withdraw rule** (mt_a6wb51enia): `withdraw_grant` takes a grantId and a required note; draft/proposed/countered only. Closes as stopped (history action "withdraw", not "stop"), open KRs archive with the note.
- **Checkpoint only at 100%** (mt_rjhwj2qggm): CHECKPOINTS = [1].
- **Rollup Needs rule** (mt_uf1bwd3exq, live): rollup:true refuses Needs naming a grant waiting on a human, an open request or a pending Town Hall report.
- **Ask to captain a goal** (PR #192, live): in-tray row + deck slide; end-to-end with a second human pending (gr_bwm0iz7rwl).

See also [dc_jcyf86dpdp](2026-10-28-web-client-panels-and-the-in-tray-yf86dpdp.md) (in-tray deck) and [dc_7lpbltjy1j](2026-10-31-rollup-37-materials-pbltjy1j.md) (rollup items 19, 21).
