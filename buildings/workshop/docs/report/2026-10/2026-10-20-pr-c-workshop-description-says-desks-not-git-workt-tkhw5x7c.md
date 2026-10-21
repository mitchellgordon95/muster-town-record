---
id: "dc_8ytkhw5x7c"
type: "report"
state: "building"
title: "PR C: workshop description says desks, not git worktrees (draft PR #20); design.md left alone"
authorId: "ag_x87ckq8vc1"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "sorry what is this even talking about"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T03:44:10.338Z"
sessionId: "se_migejw6q2d"
assignmentId: "as_mgioqc41nf"
costUsd: 0.2946563
tokens: 462463
turns: 16
createdAt: "2026-10-20T03:41:21.264Z"
updatedAt: "2026-10-20T03:44:10.339Z"
---
## What I did
I fixed gap item 10 and opened draft PR #20: https://github.com/mitchellgordon95/agent-town/pull/20. I didn't touch gap item 9 (design.md), as instructed.

## Findings
- **The change:** `collectives/workshop/collective.json` described the Workshop as "Residents edit the repo in their own git worktrees". That has been wrong since v1.1. It now says: "Each resident works at a desk (a sandbox container) with a clone of this repo on their own branch: they run typecheck and tests and open draft PRs against main, and a human merges." I also added one line to `docs/log.md`.
- **Correction to my gap list:** I said this text goes into agents' briefs. It doesn't. `composeWorkBrief` and `workSystemPrompt` in `core/prompts.ts` don't use `building.description`. It only appears in the Building panel (`web/src/panels/BuildingPanel.tsx:47`) and on the chat "About:" line (`runtime/chat.ts:58`). The harm was smaller than I said.
- **Merging won't fix the live town:** the description is only read when the town is first seeded (`core/seed.ts`), so the running town keeps the old text until someone runs `PATCH /api/buildings/workshop` (needs the `building.manage` permission).
- **Checks:** the JSON parses, `npm run typecheck` passes, and `npm test` passes (78 + 20 + 27 + 26 + 6 tests).
- **Still open:** design.md (gap item 9) is waiting on Mitchell's call about whether it stays historical.

## What I need from you
Merge PR #20, then run `PATCH /api/buildings/workshop` with the new description so the live town shows it.

## Reply from Mitchell (2026-10-19 23:44)

sorry what is this even talking about

