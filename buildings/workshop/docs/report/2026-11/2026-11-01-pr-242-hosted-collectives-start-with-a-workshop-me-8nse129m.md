---
id: "dc_pm8nse129m"
type: "report"
state: "building"
title: "PR #242 (hosted collectives start with a Workshop) merged as 6e876b7, redeploy queued; live check still to do"
authorId: "ag_dzz1h10vvd"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decisionNote: "#242 merged as 6e876b7, redeploy queued. The guest live check goes on the queue as its own assignment waiting on {deploy: 6e876b7} (chain had parked 3 times). Mitchell's keyless Start check goes in rollup 37 \"Your call\", not Needs."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-01T02:27:07.601Z"
sessionId: "se_wj562duds0"
assignmentId: "as_q1b9q9fjx9"
costUsd: 0.2824341
tokens: 14122
turns: 6
createdAt: "2026-11-01T02:26:24.624Z"
updatedAt: "2026-11-01T02:27:07.601Z"
---
## What I did
PR #242 CI finished green on head 0d1e7e1: check passed in 2m28s and the PR was mergeable/CLEAN. I merged it as 6e876b7 and queued a redeploy. I couldn't park on the deploy because this chain has already parked 3 times in a row. So the guest live check hasn't run, and [dc_7lpbltjy1j](../../wiki/2026-10/2026-10-31-rollup-37-materials-pbltjy1j.md) and [dc_pl034gahw2](../../wiki/2026-11/2026-11-01-hosted-collectives-first-run-034gahw2.md) haven't been updated yet.

## Findings
- https://github.com/mitchellgordon95/muster-town/pull/242 is merged as 6e876b7758aa4c6cd95cffd27f2e7e9c1e5fd59e. That commit should be live after the redeploy.
- The live check still to run, as a new assignment with waitFor {deploy: 6e876b7}:
  - GET https://muster.town/hollyville/api/town lists the Workshop building on gl_town with a resident.
  - /api/health commit contains 6e876b7.
  - The web bundle carries "Add your API key to start".
  
  Then add the Shipped candidate to [dc_7lpbltjy1j](../../wiki/2026-10/2026-10-31-rollup-37-materials-pbltjy1j.md) and rewrite [dc_pl034gahw2](../../wiki/2026-11/2026-11-01-hosted-collectives-first-run-034gahw2.md).
- Still needs a human (for rollup 37's "Your call"): Mitchell or a test account presses **Start a collective** without a key. They should see Workshop on the map and the HUD line "Add your API key to start". A guest can't see a hosted admin's HUD.

## What I need from you
Nothing needed.
