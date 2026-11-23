---
id: "dc_kmob9q31n9"
type: "report"
state: "building"
title: "Calibration prices a raise that can meet the hold line: PR #577 (gr_1ilvotnzta step 1), parked to merge when green"
authorId: "ag_a0hwh2rid7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-23T16:41:52.078Z"
sessionId: "se_f5gd2xnpst"
assignmentId: "as_8kaallg8m1"
costUsd: 2.5702024
tokens: 128510
turns: 50
createdAt: "2026-11-23T16:41:52.023Z"
updatedAt: "2026-11-23T16:41:52.078Z"
---
## What I did
Pulled the live step data: 42 grants with sized steps funded in the last 30 days, and the stepStates of their 74 done steps. I changed core planner.ts, grant-estimate.ts and measures.ts plus the schema, added tests on a fixture of today's data, and updated legible-delegation §7.4, invariants/grants.md #14 and log.d. Opened PR #577 (https://github.com/mitchellgordon95/muster-town/pull/577). Topic page [dc_jjbqweg1qr](../../wiki/2026-11/2026-11-23-calibration-that-cuts-grant-holds-gr-1ilvotnzta-bqweg1qr.md).

## Findings
- **Today's data reproduces the problem.** S has a median of 1.08× and a mean of 1.41× over 22 steps. M is 0.90× / 0.94× over 49. L is 0.51× over 3. The observed hold share is 62% (23 of 37 grants). The old rule would have proposed "Raise S from 50,000 to 50,000".
- **New proposal on that fixture:** "Raise S from 50,000 to 120,000 tokens. Projected hold share 46% → 24%." At 110k the projection is still above 25%, so 120k is the smallest raise that meets the line. The test asserts this.
- **How the projection works:** `projectHoldShare` is a seeded bootstrap with 400 draws per grant. Each grant keeps its real step mix, and each step's spend is drawn from the done steps of its size. Only step spend counts. The search moves in 10k steps up to the next size's price. If the step-only bootstrap is already under the line, or no raise meets it, the rule falls back to split. A size's current value is never proposed.
- **Where it shows:** `stepCalibration` rows carry `mean` and `p75` (API: /api/health stepCalibration, /api/finance/spend). The `CalibrationProposal` carries `holdBefore` and `holdAfter`. Both the brief and the adopt event line state the before and after shares.
- **Deviation from the assignment:** the ceiling margin is only an alternative line on the brief (today a 30% margin projects 22%). It is never the proposal, because the pricing table has no margin field to adopt.
- **Not known:** the gap between 62% observed and 46% projected. The likely cause is spend outside steps (PR-fix and resume sessions), which the model leaves out.
- **Checks:** typecheck passes. All core vitest files pass (185). check:docs and deadcode pass. The full `check --fast` timed out on my desk during the server tests, so CI runs those.

## What I need from you
Nothing needed.
