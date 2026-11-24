---
id: "dc_muwky84j16"
type: "report"
state: "building"
title: "gr_bre43gflz9 step 2: one Desks field, desks bound the forks, PR #600 merging on green"
authorId: "ag_b7di9b0355"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-24T22:48:59.820Z"
sessionId: "se_x64jaj4fcz"
assignmentId: "as_telks01mjm"
costUsd: 3.432348700000001
tokens: 171617
turns: 62
createdAt: "2026-11-24T22:48:59.764Z"
updatedAt: "2026-11-24T22:48:59.820Z"
---
## What I did
I built step 2 of gr_bre43gflz9 in PR #600 (https://github.com/mitchellgordon95/muster-town/pull/600, commit 3c94b4d8). Typecheck, check:docs and check:deadcode pass. Before the last test fix, the full core, server, schema, web and runtime run passed 372 of 373 files. The one failure was step-sizes.test.ts, which expected the old pricing shape. I fixed it and re-ran it, and it passes. The pre-push hook passed. The PR is parked to merge when green.

## Findings
- **Goal editor.** FundingBlock in GoalTreePanel.tsx now holds one **Desks** input, which writes goals.desksTotal through PATCH. Under it is a derived line built by `desksBuyLine` (web FreeTokens.tsx): "N desks: up to X exploration a day, Y per explorer, grants in flight no limit, N forks at once". The cap, chunk and on/off controls are gone, along with the now-unused `capText` and `desksText`.
- **Explore on/off is now one town switch, not an inherited select.** I checked the live /api/goals on 2026-11-24: no goal had explore=false, and the root had true. So no exploration-off state needed to survive. The switch is `exploreOn` (seed on) on the town defaults: PUT /api/town/defaults and a select on the Step sizes tab. When it is off, it overrides every goal. Old `explore:` ask cards still write the goal's own column, and `exploreRuleAt` still reads that column.
- **Desks bound forks.** core forks.ts has a new shell function `goalDeskBound` and a new pure function `bindingDesks`, with a fast-check property test. `freeDesks` now returns the smaller of two numbers: the free seats (headcount minus desks in use), and the fewest desks left among goals on the path that set desksTotal (desks minus live forks under that goal). The runtime's fork spawn and the explore tick both read `freeDesks`. A goal with no total counts headcount only, so desk seating on the map and visitor desks are unchanged. The stop condition did not trigger.
- **Held reason.** In the Queue tab (kanban.ts `queueLane`), building-queue work no fork has taken yet shows `held: desks full under goal "X" (gl_…): N desks, M forks running`. The explore block shows the same wording.
- **Ask acts.** Goal branches accept `desks:<n>` and `desks:none`. Old `cap:` and `explore:` actions still parse. Docs updated: goals.md "Effort steering is desks", how-work-gets-done.md §8 and the desks-per-subtree section, legible-delegation.md's list of acts, and a log.d entry.
- **Not done:** the mock server still uses a flat MOCK_CAP fixture for the cap. Nothing has been checked live yet. Once PR #600 is live, a human checks kr_fkn4tgsp59 (the Desks field) and kr_gj2qmiqtov (set desks below the live forks, read the Queue tab) in the browser.

## What I need from you
Nothing needed.
