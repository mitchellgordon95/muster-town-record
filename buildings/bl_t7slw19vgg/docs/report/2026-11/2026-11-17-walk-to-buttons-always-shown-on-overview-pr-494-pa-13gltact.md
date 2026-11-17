---
id: "dc_dh13gltact"
type: "report"
state: "building"
title: "Walk-to buttons always shown on Overview: PR #494, parked on CI to merge"
authorId: "ag_9qxjdb8pij"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-17T04:08:15.637Z"
sessionId: "se_32mztqde69"
assignmentId: "as_41atjg45kq"
costUsd: 0.4811323999999999
tokens: 24057
turns: 12
createdAt: "2026-11-17T04:08:15.632Z"
updatedAt: "2026-11-17T04:08:15.637Z"
---
## What I did
I removed the "Go to: …" fold from a building's Overview tab. The change is in PR #494 (https://github.com/mitchellgordon95/muster-town/pull/494), head 3f436dd9, marked ready. Typecheck is green and buildingTabs.test.tsx passes (3/3). The session is parked on CI so the PR can be squash-merged on green. There is no redeploy: CI deploys it.

## Findings
- `packages/web/src/panels/BuildingPanel.tsx`: the `<details className="walk-fold">` / `<summary>` is gone, and so is the module-level `walkOpen`. The `.walk-links` buttons now render directly under the goal summary. These are the board, filing cabinet, manager's desk with the "N waiting" pill, hydrant with its pill, meeting table, goal tree, and Edit layout for managers. The Edit-layout permission check is now one `canEditLayout` const.
- `styles.css`: the three dead `.walk-fold` rules are deleted. `.walk-link` changed to `flex: 1 1 200px; max-width: calc(50% - 4px)`, which lays the buttons out two per row in a wrapped grid instead of one tall column. This applies on a laptop and in the phone sheet.
- I did not touch the Talk-to-manager / Plant-a-flag row or the schedule `.kr-more` fold.
- No test asserted the summary line. I added the log entry docs/log.d/2026-11-17-teo-2-uncollapse-walk-links.md.
- After the merge, the live commit should be the squash of #494. When Mitchell opens a building's Overview tab, he will see the walk-to buttons straight away in two columns, with no click to unfold them.

## What I need from you
Nothing needed.
