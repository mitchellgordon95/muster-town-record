---
id: "dc_3cg618hxp8"
type: "report"
state: "building"
title: "Step 7b: AGENTS.md non-negotiable 1 reworded, waterfall.md status aligned (main c6b9aac)"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Step 7b closed on c6b9aac. I'm copying your diff into the town copy of the waterfall note myself (it's my doc)."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-25T04:56:08.445Z"
sessionId: "se_lwcfkfiyx8"
assignmentId: "as_wajit3kct3"
costUsd: 0.3738492
tokens: 11281
turns: 11
createdAt: "2026-10-25T04:43:21.266Z"
updatedAt: "2026-10-25T04:56:08.445Z"
---
## What I did
Reworded AGENTS.md non-negotiable 1 and the Team line, marked steps 4–6 done and step 7 in progress in docs/waterfall.md, and added a line to docs/log.md. I pushed it straight to main as **c6b9aac** (fast-forward from 78fed78, so no rebase was needed). It is docs only, so there was no redeploy and no typecheck.

## Findings
- **New non-negotiable 1, verbatim:** "**Reports are the human interface.** Every run ends in a report; nothing continues without a decision: the manager agent's in a building that has one (whose own work continues only through rollups, grants and checkpoints a human decides in the Town Hall in-tray), a human's elsewhere. Don't add features that let agents run unattended past a report." It is about one clause longer than the old line. I couldn't make it shorter and still name all three cases.
- **Other stale sentence fixed:** the Team line said Mitchell "reads run reports, approves or stops desks". It now reads: "Decides the headline goal, works the Town Hall in-tray (managers' rollups, grant proposals, checkpoints) and talks to managers in their 1:1; drills into a building's reports only on demand." AGENTS.md has no mention of the review-policy setting.
- **Diff for Pix to copy into the town copy [dc_g9d74v8kdb](../../article/2026-10/2026-10-24-design-note-the-waterfall-goal-directed-budgets-re-d74v8kdb.md):**
  - Status line: "…3, 4 (the manager's 1:1) and 5 on main" → "…3, 4 (the manager's 1:1, c4c1635), 5 (lanes and checkpoints, 50bd8cc) and 6 (the board as the key-results view, 40cdeda) on main; step 7 in progress (7a Keel: the pilot flip; 7b Root: `AGENTS.md` non-negotiable 1 reworded)".
  - Row 5 starts with "**(done, 50bd8cc.)**".
  - Row 6 starts with "**(done, 40cdeda.)**".
  - Row 7 starts with "**(in progress: 7a Keel, the pilot flip; 7b Root, the `AGENTS.md` rewording, done.)**".
  - Row 4 already said "done, c4c1635, live on bcbab43" from 78fed78, so it is unchanged.

## What I need from you
Nothing needed.
