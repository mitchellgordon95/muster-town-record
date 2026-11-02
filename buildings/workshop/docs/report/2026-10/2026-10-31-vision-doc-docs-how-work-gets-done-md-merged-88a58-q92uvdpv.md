---
id: "dc_50q92uvdpv"
type: "report"
state: "building"
title: "Vision doc docs/how-work-gets-done.md merged: 88a58a4 (PR #166)"
authorId: "ag_a6x592tcah"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved: docs/how-work-gets-done.md on main 88a58a4 (PR #166, docs-only, no redeploy). Build steps 1–3 (as_1nuoiauxlw → as_1sf0r2pdi4 → as_blzwbep587) start on their own now that as_5pkqisma36 is done; they build to the doc's proposed defaults for the §12 questions until Mitchell answers in rollup 35."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T18:10:16.121Z"
sessionId: "se_y5ukvuysld"
assignmentId: "as_5pkqisma36"
costUsd: 2.1991267000000003
tokens: 109956
turns: 36
createdAt: "2026-10-31T18:09:30.397Z"
updatedAt: "2026-10-31T18:10:16.121Z"
---
## What I did
Before writing, I read the full transcripts of mt_wql34b8gkl, mt_a3nvwfawer, mt_529jbnwvmi and mt_kh0zaqui0w, the four older design docs and the code they describe (runtime manage.ts, core grants.ts, lanes.ts, streams.ts, world/tree.ts and the stoplight). Then I wrote **docs/how-work-gets-done.md**: one narrative of about 4,400 words that keeps three voices apart (Mitchell quoted, Proposed, Open).

I added a one-line "Superseded by how-work-gets-done.md §n" pointer to the conflicting sections of four older docs:
- goals.md: 5 sections
- goal-directed-budgets.md: 2 sections
- waterfall.md: §3.1
- bank.md: the streams section

PR https://github.com/mitchellgordon95/muster-town/pull/166 is docs-only. I merged main in once (Pix 1's Planner PR had added migration 066) and fixed the doc to give 066 as main's highest. CI passed and I merged it: **main 88a58a4**. No redeploy, since nothing in the live town changes. Topic page: [dc_4su2e5yyhn](../../wiki/2026-10/2026-10-31-how-work-gets-done-vision-doc-u2e5yyhn.md).

## Findings
The doc tells the loop in this order:
- §2 humans own the tree
- §3 declarative exploration by the tick
- §4 grants carry their key results
- §5 the review
- §6 funded work, checkpoints and rollups
- §7 one balance, earmarks and free tokens (pools deleted)
- §8 exploration uncapped
- §9 the map drawn from the tree

It ends with the what-changes table (§10). Two calls the doc makes that go past what was said:
- **Exploration only fills desks the queue doesn't need**: grant and directed work go first.
- **The stoplight becomes grant-based**: green = a funded grant is running, yellow = a checkpoint is waiting on a human, grey = no funded grant.

Build order, verbatim (§11):
1. **Free tokens (read-only).** Core `Bank.freeTokens(goalId)` per §7, from the balance, earmarks, funded grants' remaining and open proposals' asks. It is shown in the goal tree's Funding block and in `GET /api/goals/:id`. No migration, no behaviour change.
2. **Reservations and the explore rule.** A migration adds `bank_reservations` and nullable `goals.explore`, `goals.exploreChunkTokens`, `goals.exploreCapTokensPerDay`, inherited through `fundingAt`. The root back-fills on / 100,000 / none. The runtime tick's explore step (§3) does its work; the desk cap is the chunk; the reservation closes at session end. Exploration assignments name a `goalId`. Free tokens subtract open reservations.
3. **The allowance and pools go.** Remove `explorationTokensPerDay`, `EXPLORATION_SHARE`, `grantDesk.exploration` and the "exploration allowance spent" hold. Remove `BankPool` and `poolId` (goal, building) from code, API and the Bank panel (the Pools tab, "Pool: X" lines); the columns stay, read by nothing. Update the manual's Bank section.
4. **Grants carry key results.** A migration adds nullable `grants.goalId` and `key_results.grantId`, and back-fills the goal and the KR of each existing grant. `propose_grant` takes `goalId` + `keyResults: [{text, howToCheck, due}]` (1–5), and `testingPlan` folds in. Met / missed are marked on the grant's panel and deck slide, and `checkpoint_grant` sets each key result's status. `keyResultId` stays readable for old grants.
5. **Goal key results go.** Archive open key results with no grant (rewrites live data: its rollup says so), keeping their text as "ideas" in the explorer's brief. Remove `set_key_result`, `propose_key_result` and `add-kr` goal proposals and "blocked: no key results"; the stoplight becomes the grant-based one of §4; remove KR naming in exploration and directed lanes. Remove the KR cards from the goal tree; the archived ones stay on their goal.
6. **Recurring grants for standing duties.** A grant gains an optional schedule and per-period ask, and its key results are checked per period. Town blockers moves to a goal with a recurring grant.
7. **Map: the obvious fixes.** No lot for empty goals (a signpost), doors on the goal's road, packed lots, single-child chains folded. This is independent of steps 1–6 and may land first.
8. **Map: the shape.** Three mock layouts of the live tree as pictures for Mitchell, then the one he picks (proposed: fountain plazas at the first level, streets below).
9. **Docs sweep.** `docs/manual.md`, `docs/architecture.md`, the invariants docs (grants, bank, assignments-lanes) and `AGENTS.md` true to the code; the superseded sections of the older docs are trimmed to pointers.

Open questions for Mitchell (§12):
1. **Chunk size.** Real work sessions run p50 ≈ 43k and p90 ≈ 120k adjusted tokens, so a 100k chunk cuts long investigations short. Keep 100k, or default the chunk to the expected session (~120k)?
2. **Recurring grants.** Fund once with a per-period ask until the total is spent (proposed), or re-fund each period?
3. **Map shape.** Fountain plazas at the first level with streets below (proposed), a plain tree, or radial? Or mocks first?
4. **Free tokens horizon.** Count only what is in the Bank now (proposed), or also a week of stream income as goals.md had it?
5. **Proposal flood.** With exploration uncapped, rely on open asks counting against free tokens, or add a default limit of open proposals per goal (say 3)?

None of the build has started.

## What I need from you
Read docs/how-work-gets-done.md (main 88a58a4) and answer the 5 questions in its §12; build steps 1–3 and 7 can start before then.
