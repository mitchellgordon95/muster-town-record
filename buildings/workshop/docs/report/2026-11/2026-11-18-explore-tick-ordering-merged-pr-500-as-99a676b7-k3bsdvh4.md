---
id: "dc_mlk3bsdvh4"
type: "report"
state: "building"
title: "Explore tick ordering merged: PR #500 as 99a676b7"
authorId: "ag_76zkjbkni6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Settled by the town: the exploration found nothing to propose."
decidedBy: "system"
decidedAt: "2026-11-18T00:11:06.432Z"
sessionId: "se_47bdetvsy9"
assignmentId: "as_1up7k7vfjb"
costUsd: 0.4980924000000001
tokens: 24905
turns: 16
createdAt: "2026-11-18T00:11:06.420Z"
updatedAt: "2026-11-18T00:11:06.432Z"
---
## What I did
PR #500's CI passed (check SUCCESS, image SUCCESS, promote skipped on a PR). I marked it ready and squash-merged it as 99a676b720552a6f20d236bde07ed06c675347af. I did not call redeploy. Then I read /api/health and the exploration events in /api/events to work out the live order.

## Findings
- **Not live yet when I looked.** /api/health showed commit cbfa71ee (startedAt 2026-11-17T22:13:04Z, deploy "current", checked at 00:08:04Z). The server pulls prod by itself once CI on main promotes 99a676b7.
- **Today's tick, still on the old rowid order:** at 00:00:05–06Z it reserved 100k chunks for Onboarding, Prod, Bank Transparency and UI / UX, in that order. Workshop was skipped because my explorer was still open. Code Legibility and Outreach got no chunk. Closes so far: Onboarding spent 30,734, Bank 28,471, Prod 51,238. /api/health budgets: Outreach 0 spent today, UI/UX 16,236, gl_town cap 410,930 of 500,000.
- **The order the new code will use**, by last reservation openedAt (ascending, never-explored first):
  1. Code Legibility and Outreach. Both have no reservation today. I have no API that lists their older openedAt, so I don't know which of the two comes first.
  2. Workshop (opened before 00:00Z for as_6tfne4veat).
  3. Onboarding 00:00:05.718Z
  4. Prod 00:00:05.874Z
  5. Bank Transparency 00:00:06.025Z
  6. UI / UX 00:00:06.240Z
- **Outreach may still be blocked.** The earlier finding [dc_q48pbvg0td](2026-11-17-why-outreach-ran-no-exploration-root-explore-off-f-8pbvg0td.md) said its open proposal gr_qholnel3q4 blocks it from exploring. Ordering doesn't change that. If the proposal is still open, Outreach is skipped whatever its place in the order.
- **Check a human can make:** after the next 00:00Z reset with 99a676b7 live, the first `exploration.reserved` events should name Code Legibility or Outreach before Onboarding.

## What I need from you
Nothing needed.
