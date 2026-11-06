---
id: "dc_bey780gdew"
type: "report"
state: "building"
title: "Hollyville retire merged: PR #353 = dc1fcbf, live once CI promotes it"
authorId: "ag_p9mij6t4x3"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Done: #353 merged as dc1fcbf, CI promotes it (no redeploy, per the Prod FYI). Mitchell's click path goes into rollup 49's Hollyville \"Your call\" once dc1fcbf is live, alongside the rename (#355) and the bulletin board."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-05T19:06:59.631Z"
sessionId: "se_j2quy35fzm"
assignmentId: "as_8obvgooj2m"
costUsd: 0.2444871
tokens: 12224
turns: 4
createdAt: "2026-11-05T19:06:36.604Z"
updatedAt: "2026-11-05T19:06:59.631Z"
---
## What I did
- PR #353's CI was green: check passed, image passed, promote skipped. I marked the PR ready and merged it at 19:06:29Z. The merge commit is **dc1fcbf11f852cbc9111d80735473efd55394a2c**.
- I did not call `redeploy`. CI's promote job takes this commit live.

## Findings
- At 19:06:31Z, /api/health still showed live = 1edf24dc. dc1fcbf is not live yet; CI will promote it.
- Once it is live, Mitchell clicks: **muster.town/workshop → Planning desk → System → Hosted collectives → Retire… next to Hollyville → Retire Hollyville for good.**
- Retire is not a hard delete. What it leaves behind:
  - The hub.db row stays with state 'retired', and the slug is never reused.
  - /hollyville/ returns 410, and the homepage stops listing Hollyville.
  - hosted/hollyville/ stays on disk, along with its backups.
- PR: https://github.com/mitchellgordon95/agent-town/pull/353

## What I need from you
Once dc1fcbf is live, Mitchell clicks the path above to retire Hollyville.
