---
id: "dc_uu8dydatjl"
type: "report"
state: "building"
title: "PR #297 merged as 7a5a164 (key results auto-met on close); redeploy queued"
authorId: "ag_tqbjh98wsc"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "PR #297 merged as 7a5a164, redeploy queued. A live check waits on {deploy: 7a5a164}; rollup 44 (not before ~06:45Z) carries the \"flip any wrongly auto-met key result to missed\" line as its Your call."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-04T02:59:19.147Z"
sessionId: "se_9bjk5g7x3w"
assignmentId: "as_dg64263mu9"
costUsd: 0.45787979999999995
tokens: 22894
turns: 9
createdAt: "2026-11-04T02:59:01.509Z"
updatedAt: "2026-11-04T02:59:19.147Z"
---
## What I did
PR #297's CI passed: `check` ran in 3m4s and `promote` was skipped. GitHub said the PR was mergeable, and migration 087 is still the only 087 on main (the highest there was 086). I marked the PR ready and merged it as **7a5a164**. Typecheck on the merged main is clean. I queued a redeploy, so **7a5a164 should be live** once the server restarts; I have not checked it this session. Item 27 on the Rollup materials page [dc_7lpbltjy1j](../../wiki/2026-10/2026-10-31-rollup-37-materials-pbltjy1j.md) is updated.

## Findings
- https://github.com/mitchellgordon95/muster-town/pull/297 is merged into main as 7a5a164. It builds on a092a79, which includes #296.
- Once the deploy runs, closing a grant as done marks its open key results met and archives them. The Town Hall in-tray and the review deck no longer have a "mark met or missed" row or slide.
- **Migration 087 changes live data:** the 13 closed-as-done grants whose key results are still "claimed" get them set to met, and those grants drop out of the in-tray. A funder can still flip any of them to "Mark missed" (a why is required) or "Back to met" on the grant page.
- There is no picture because the change is in the API and in-tray only.
- Rollup 44 (item 27) should confirm 7a5a164 is live, using GET /api/health and `git merge-base --is-ancestor`, before calling it shipped.

## What I need from you
Nothing needed. After the deploy, flip any of the 13 auto-met key results that didn't actually ship to missed on its grant page.
