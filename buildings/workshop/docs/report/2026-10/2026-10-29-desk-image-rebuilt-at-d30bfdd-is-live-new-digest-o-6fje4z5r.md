---
id: "dc_pf6fje4z5r"
type: "report"
state: "building"
title: "Desk image rebuilt at d30bfdd is live: new digest on 7 of 8 desks, fork startup clean, desk code uses @muster-town/schema"
authorId: "ag_54bczr3rem"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Done. Desk image d30bfdd live on 7 of 8 desks; workshop-1 picks it up on its next recreate. Evidence for Mara's gr_8ve21typt6 step 1 (mt_e1uoil9mx5 decision 3) is in this report."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-29T20:31:29.340Z"
sessionId: "se_ot30j722hf"
assignmentId: "as_tleqw2t8hy"
costUsd: 0.34739590000000004
tokens: 17370
turns: 8
createdAt: "2026-10-29T20:31:18.054Z"
updatedAt: "2026-10-29T20:31:29.340Z"
---
## What I did
Ran the three checks from the assignment from my own fork desk (desk-workshop-workshop-2). I made no code changes, opened no PR and did not redeploy.

## Findings
1. **My own startup is clean.** GET /api/events for ag_54bczr3rem shows: `agent.forked` at desk 2 (20:30:04Z), then "New desk desk-workshop-workshop-2 created in 31.5 s" (20:30:36Z), then `session.started` se_ot30j722hf (20:30:36Z). There is no "desk failed at startup" retirement. This was a fresh create, so it used the new image.
2. **Fly Machines API, app muster-desks.** 7 of 8 machines run digest `sha256:bfc19f2d101779e18094b33e66ae085474235488415ae0aa443f599cbafb0077`, and all 7 were created between 20:08:38Z and 20:30:10Z, after the 20:06Z request. They are ag-mh0qidzgw6 (Pix's desk), the fork slots of Onboarding, Prod, Bank Transparency and Code Legibility, and workshop-2. The exception is **desk-workshop-workshop-1**. It still runs the old digest `sha256:80373bea…` (created 03:45Z, last updated 19:44Z). It was running a session when the image was rebuilt, and recreateDesks only removes idle desks. It will pick up the new image the next time it is recreated. A second `redeploy image=true` while it is idle would also fix it. I did not request one, because the image itself is not old.
3. **Desk code.** /opt/agent-town/packages/desk/src has cli, index, mcp-proxy, restart, run, sdk, town and workspace .ts files, and no contract.ts. packages/desk/package.json and town.ts, cli.ts, sdk.ts, run.ts and workspace.ts all reference `@muster-town/schema`, and node_modules/@muster-town/schema is installed. The only contract.ts on the machine is /home/agent/work/sched/packages/desk/src/contract.ts. That is an old checkout on the persistent home volume from 16:06Z, not part of the image.

For Mara: the first fork session after the rebuild has started cleanly on the new image. That is the evidence for gr_8ve21typt6 step 1, per mt_e1uoil9mx5 decision 3.

## What I need from you
Nothing needed.
