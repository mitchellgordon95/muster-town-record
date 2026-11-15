---
id: "dc_335f6gp04t"
type: "report"
state: "building"
title: "PR #461 merged (7d86da65): needs with no ask leave the queue and deck"
authorId: "ag_45kzuynqnz"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Settled by the town: the request is done."
decidedBy: "system"
decidedAt: "2026-11-15T22:08:10.785Z"
sessionId: "se_3otl3qup4x"
assignmentId: "as_j07mah3ryb"
costUsd: 0.24269469999999999
tokens: 12135
turns: 4
createdAt: "2026-11-15T22:08:10.774Z"
updatedAt: "2026-11-15T22:08:10.785Z"
---
## What I did
Checked PR #461's CI. `check` and `image` passed, and `promote` was skipped as it is on PR runs. The PR was mergeable. I looked at its file list against main: it adds no migration and touches no `migrations/` file. I marked it ready and merged it. Merge sha: **7d86da65c22de8f81059ca696153ca43e62badc1**. I did not call redeploy. CI deploys green main by itself.

## Findings
- PR #461 is merged as 7d86da65 (https://github.com/mitchellgordon95/muster-town/pull/461).
- Once 7d86da65 is live, a proposed or held grant with no ask no longer has a row in the decision queue. The human sees one plain line under the queue with nothing to press, e.g. "Proposal from Prod: its card is being written." The review deck works the same way. Such a grant gets no slide of its own and appears on the state-of-the-town slide as "Not yet on a slide: …". When the ask is filed, it gets its row and slide as before.
- The Secretary's ledger-rule card now recommends Add, so the structure warning goes away.
- I have not checked it live. When this report was filed, /api/health did not yet show 7d86da65.

## What I need from you
Nothing needed.
