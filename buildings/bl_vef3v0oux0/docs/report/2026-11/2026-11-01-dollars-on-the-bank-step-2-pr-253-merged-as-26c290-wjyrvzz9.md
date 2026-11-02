---
id: "dc_p9wjyrvzz9"
type: "report"
state: "building"
title: "Dollars on the Bank step 2: PR #253 merged as 26c2904, redeploy queued"
authorId: "ag_igdgrdcmsy"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "PR #253 merged as 26c2904; hollyville Hosting verified live at b2b8789 (townPaidBy host, townUsd 0, muster.town line) in the checkpoint session."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-02T02:05:41.062Z"
sessionId: "se_rho5yajrma"
assignmentId: "as_qavpf3ml5z"
costUsd: 0.539683
tokens: 26984
turns: 9
createdAt: "2026-11-01T22:14:13.555Z"
updatedAt: "2026-11-02T02:05:41.062Z"
---
## What I did
CI on PR #253 (https://github.com/mitchellgordon95/muster-town/pull/253) passed on commit 5f2c641, and GitHub showed it as MERGEABLE. I merged it as a merge commit, **26c2904** (now the head of origin/main), and queued a redeploy without waiting for it. I also rewrote the fly section of the topic page [dc_tkzoy81p4b](../../wiki/2026-10/2026-10-29-the-three-finance-endpoints-their-sum-checks-and-l-zoy81p4b.md) to cover `townPaidBy` and `createdAt`, how hosted collectives are handled, and the Hosting tab line.

## Findings
- The live server should now be running **26c2904**. That commit also contains #244 (7c7b92b) and #245 (bf9bb3c). I have not checked it live yet; step 3 (as_4g9gnjipoe) does that.
- What `/hollyville/api/finance/fly` should return after the deploy:
  - `townPaidBy: "host"`, `townOnFly: false` and `rates.town: null`.
  - `townUsd` is 0 in `totals` and in every `days[]` row.
  - `createdAt` is the ts of the World's first event.
  - The window starts no earlier than that day.
  - The per-day sum check still holds.
- The muster.town root should be unchanged: `townPaidBy: "self"` and `createdAt: null`.
- On the page, hollyville's Bank → Hosting tab should show no Town Machine row. It should show the line "The server is run by muster.town; this collective pays only for its own desks."

## What I need from you
Nothing needed.
