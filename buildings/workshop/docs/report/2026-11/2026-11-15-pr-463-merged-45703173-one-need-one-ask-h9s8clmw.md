---
id: "dc_onh9s8clmw"
type: "report"
state: "building"
title: "PR #463 merged (45703173): one need, one ask"
authorId: "ag_9nb225kwuw"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Settled by the town: the request is done."
decidedBy: "system"
decidedAt: "2026-11-15T22:20:27.887Z"
sessionId: "se_lti24do3hv"
assignmentId: "as_czlhp5k8df"
costUsd: 0.296615
tokens: 14831
turns: 6
createdAt: "2026-11-15T22:20:27.876Z"
updatedAt: "2026-11-15T22:20:27.887Z"
---
## What I did
PR #463's CI was green (check SUCCESS, image SUCCESS) and its merge state was CLEAN. Main was ahead by one PR, #462 (Secretary rest spot). That PR touches only layout/furniture/town-hall-rests files, none of which #463 changes. #463 adds no migrations. I marked #463 ready and merged it without merging main in again. I did not call redeploy; CI deploys main.

## Findings
- **Merged as 45703173a0b5869cff930b6c1ded247f87c0e61a** (https://github.com/mitchellgordon95/muster-town/pull/463). This ships Mitchell's decisions 2 and 3 from mt_dwsxo7oms8 as Pix 2 built them ([dc_ytjak780xc](2026-11-15-duplicate-asks-decisions-2-3-pr-463-open-parked-on-jak780xc.md)).
- **What a human sees when two asks are filed on one need:** one card in the queue, unchanged. The second filer's words appear as one `ask-refused` entry on the job's thread. The card is marked THREAD MOVED so its owner can rewrite it whole.
- **Managers:** `ask` with askId plus a whole card rewrites the building's own ask. With withdraw and a note, it retires the ask. Asks of other buildings are refused.
- **Secretary:** `rank fold` folds one ask into another.
- **Not checked yet:** whether the change is live. Health has not been read for 4570317.
- **Unblocked:** as_3f4qsq15tt (decision 4) was queued behind as_c90hwgtrpj and can start now.

## What I need from you
Nothing needed.
