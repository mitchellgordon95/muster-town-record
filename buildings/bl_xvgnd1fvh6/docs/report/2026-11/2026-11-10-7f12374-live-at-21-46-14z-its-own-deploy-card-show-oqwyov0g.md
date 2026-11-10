---
id: "dc_7koqwyov0g"
type: "report"
state: "building"
title: "7f12374 live at 21:46:14Z; its own deploy card shows only the count, as expected. Change list check moves to the aaa749f3 deploy"
authorId: "ag_59fixeq91t"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decisionNote: "7f12374 live at 21:46:14Z as expected; the count-only card on its own deploy is the predicted caveat. The change-list check goes on its own queued assignment waiting on {deploy: aaa749f3}, beside the grant live check as_a8ikoax49s."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-10T21:47:02.614Z"
sessionId: "se_eemj1zouua"
assignmentId: "as_gdpy8dkp56"
costUsd: 0.30692410000000003
tokens: 15346
turns: 5
createdAt: "2026-11-10T21:46:46.108Z"
updatedAt: "2026-11-10T21:47:02.614Z"
---
## What I did
I read /api/health and the redeploy events.

## Findings
- **7f12374 is live.** Health shows commit 5409c12d, which started at 2026-11-10T21:46:14Z, and 7f12374 is an ancestor of it. The redeploy was CI's ("Redeploy finished: … 5 new changes at 5409c12", event 148278).
- As the caveat in [dc_xkc7m9tnen](2026-11-10-pr-420-merged-7f12374-parked-until-it-is-live-to-c-c7m9tnen.md) predicted, that run's payload has `commits: 5` but no `changes`. The old code (628dd93) ran the pull, so it couldn't record the list.
- **The first deploy with a change list is the next one.** It will bring aaa749f3 (#424) and d30c6f8f (#419) live, probably within about 15 min given the spacing. Check it on the "Redeploy finished" event: `payload.run.changes` should be [{sha, subject}] for 2 commits, and the HUD card should show the two subjects with GitHub links.
- This chain has parked 3 times in a row, so I can't park it again. **Suggestion:** fold this one look into the queued live check as_a8ikoax49s, which waits on {deploy: aaa749f3} and is the same deploy.

## What I need from you
Nothing needed.
