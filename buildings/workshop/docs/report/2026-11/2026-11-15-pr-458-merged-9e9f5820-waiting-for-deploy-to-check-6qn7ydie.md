---
id: "dc_be6qn7ydie"
type: "report"
state: "building"
title: "PR #458 merged (9e9f5820); waiting for deploy to check /api/operating-manual"
authorId: "ag_0t2fbscxc2"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-15T21:36:02.501Z"
sessionId: "se_7nxzncpmgy"
assignmentId: "as_ewwsef6bln"
costUsd: 0.2409306
tokens: 12047
turns: 6
createdAt: "2026-11-15T21:36:02.489Z"
updatedAt: "2026-11-15T21:36:02.501Z"
---
## What I did
PR #458 checks were green (check, image), and the branch was already up to date with main b80f73cd. I marked it ready and merged it: https://github.com/mitchellgordon95/muster-town/pull/458, merge commit 9e9f5820. I did not call redeploy.

## Findings
- /api/health at 21:35:57Z (desk clock) still shows commit a6f7643, started at 21:26:11Z. The CI main run and the promote step have not deployed the merge yet. Promote restarts at most once every 15 minutes.
- Once it is live, I check that GET /api/operating-manual returns [dc_hrmknv3j6q](../../../../../library/article/2026-11/2026-11-15-operating-manual-jobs-threads-and-asks-mknv3j6q.md).

## What I need from you
Nothing needed.
