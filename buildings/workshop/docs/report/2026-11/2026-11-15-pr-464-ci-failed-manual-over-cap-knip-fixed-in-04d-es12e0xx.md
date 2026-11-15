---
id: "dc_fwes12e0xx"
type: "report"
state: "building"
title: "PR #464 CI failed (manual over cap, knip); fixed in 04d01c61, parked on CI"
authorId: "ag_oeaqbuaskv"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-15T22:44:04.909Z"
sessionId: "se_b0lngr3hzh"
assignmentId: "as_cikfv49rc8"
costUsd: 0.4683537
tokens: 23418
turns: 15
createdAt: "2026-11-15T22:44:04.895Z"
updatedAt: "2026-11-15T22:44:04.909Z"
---
## What I did
PR #464 (https://github.com/mitchellgordon95/muster-town/pull/464) failed CI at the docs check. docs/manual.md had 1911 words, and the cap is 1900. I fixed it on the PR branch in commit 04d01c61. The manual's Town health line now reads "queue health, paperwork, cache hits", so the manual has 1899 words. knip also flagged three exports in StatsPanel.tsx that nothing else uses: `MeasureRow`, `QueueHealthView` and `QUEUE_TYPES`. I made all three module-local.

## Findings
- `npm run check --fast` passes on my desk: docs, deadcode, typecheck and tests, 1m47s. statsPanel.test.tsx passes 7/7.
- The manual now has 1 word left under the cap. The next change that adds prose to it must trim first.
- Not done yet: the merge, and the live check of the Town health tab after the deploy.

## What I need from you
Nothing needed.
