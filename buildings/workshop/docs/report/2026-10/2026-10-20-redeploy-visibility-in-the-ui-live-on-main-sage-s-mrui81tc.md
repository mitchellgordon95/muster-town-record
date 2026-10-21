---
id: "dc_4umrui81tc"
type: "report"
state: "building"
title: "Redeploy visibility in the UI: live on main (Sage's 26a7698 + my 39562ae)"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T18:56:33.740Z"
sessionId: "se_3ej3de8mea"
assignmentId: "as_ov41jfhe0p"
costUsd: 0.3255917
tokens: 375761
turns: 13
createdAt: "2026-10-20T18:53:38.586Z"
updatedAt: "2026-10-20T18:56:33.740Z"
---
## What I did
I replied to Mitchell, then checked main. Sage had already shipped most of this in 26a7698, 8 min before the request. Typecheck passes, and the 16 redeploy tests in runtime and web pass. I filled one gap, pushed straight to main, ran a redeploy and told Mitchell what to look for.

## Findings
What Mitchell asked for, and what now covers it:
- **Scheduled:** a HUD notice for everyone: "Redeploy scheduled: N changes waiting; restarts when X sessions finish (names)". It updates as the sessions it waits on change.
- **Who's waiting for it:** agents whose work the drain holds get a "⟳ redeploy" pill on the map. My commit 39562ae makes the HUD name them ("Lena waits for it") instead of only counting them.
- **Finished:** the restarted server posts "Redeploy finished: N new changes". The client refetches events on reconnect, shows a toast, and keeps a green notice up for 10 min. A failure shows a red notice and toast that link to the planning desk log.

I verified the change with typecheck and the updated test in `packages/web/test/redeploy.test.ts`. No PR: the standing rule is to push to main.

## What I need from you
Nothing needed.
