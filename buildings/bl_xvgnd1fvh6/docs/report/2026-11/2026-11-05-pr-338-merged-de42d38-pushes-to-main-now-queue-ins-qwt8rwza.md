---
id: "dc_jaqwt8rwza"
type: "report"
state: "building"
title: "PR #338 merged (de42d38): pushes to main now queue instead of cancelling; parked on deploy"
authorId: "ag_8oco7x7h8w"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "PR #338 merged as de42d38 without a redeploy; prod already past the storm (live aa6f4fb). The parked {deploy: de42d38} wait keys on the running server's commit (packages/core/src/waits.ts:78 → runtime hostIsLive), and promote skips the restart for a .github/-only change (ci.yml:80-84), so it only resolves when the next runtime commit deploys; replacing it with a timed check."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-11-05T00:01:29.426Z"
sessionId: "se_bmmk1dum2f"
assignmentId: "as_bi5d7y217b"
costUsd: 0.28907710000000003
tokens: 14454
turns: 5
createdAt: "2026-11-05T00:00:37.849Z"
updatedAt: "2026-11-05T00:01:29.426Z"
---
## What I did
- PR #338's CI was green (check SUCCESS, run 41894913494). I marked it ready and merged it with a merge commit: **de42d38**. The diff is one line in .github/workflows/ci.yml: `cancel-in-progress: ${{ github.event_name == 'pull_request' }}`, plus a comment.
- I did not call redeploy. Parked on {deploy: de42d38}.

## Findings
- **The storm calmed on its own before this merge.** On main, run 41902872214 (#348, started 20:03:18Z) and run 41906335628 (#349, started 20:24:39Z, 15m36s) both succeeded. Two runs were still cancelled in between (#346 and #347 at 19:55Z, #345 at 20:10Z). That cancelling is what #338 stops from now on.
- **Prod is past ad27e6f.** origin/prod = aa6f4fb (merge of #349). Live /api/health reports commit aa6f4fb, started 2026-11-04T20:40:25Z.
- **Which commit should be live:** de42d38, once its ci run on main goes green and promote moves prod. The change only touches .github/, so promote may skip the restart (its rule skips restarts for .github/-only changes). In that case `prod` moves but the health commit can stay at aa6f4fb. The next session should check `origin/prod` contains de42d38, and not rely on health alone. If the deploy wait never resolves for that reason, that is the explanation.

## What I need from you
Nothing needed.
