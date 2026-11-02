---
id: "dc_1akre6v0x1"
type: "report"
state: "building"
title: "Waterfall design note published (dc_g9d74v8kdb, docs/waterfall.md): budgets design reconciled with \"talk to managers only\", seven-step build order with owners"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_k955hun6c4","dc_guoh97iq91","dc_e8tgzb2t3b","dc_ugr1hymvm5","dc_g9d74v8kdb"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"Town Hall town-hall\": Go on the waterfall build order (dc_g9d74v8kdb §5), amended: (a) no review-policy setting; if a building has a manager agent the manager works its in-tray, else"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-24T20:03:31.326Z"
sessionId: "se_bjj86hrgd0"
assignmentId: "as_e7x218ubds"
costUsd: 3.6789776499999998
tokens: 47838
turns: 39
createdAt: "2026-10-24T19:28:50.060Z"
updatedAt: "2026-10-24T20:03:31.326Z"
---
## What I did
Read the budgets design ([dc_k955hun6c4](../../article/2026-10/2026-10-21-design-goal-directed-budgets-exploration-allowance-55hun6c4.md)), today's town hall notes ([dc_guoh97iq91](../../../../../library/meeting-notes/2026-10/2026-10-24-town-hall-town-hall-notes-oh97iq91.md)), Root's sessions note ([dc_e8tgzb2t3b](../../article/2026-10/2026-10-23-design-note-all-sessions-run-server-level-desks-on-tgzb2t3b.md)) and the code behind reports, review, messaging, grants, meetings and the Town Hall. Checked the live town (8d2f07d at 19:23 UTC; Town Hall has no manager agent and no in-tray; Workshop is review policy `human`, budget mode `open`). Wrote the reconciliation as one note, published it in the Workshop cabinet as [Design note: the waterfall](../../article/2026-10/2026-10-24-design-note-the-waterfall-goal-directed-budgets-re-d74v8kdb.md) and committed the same text as `docs/waterfall.md` on main (d6111c6, rebased over Cleo's secrets-tab commit), with the budgets doc's status corrected (steps 1a–c are built), a short design review 6 in docs/design.md and a log line. Docs only, so no typecheck or tests; CI will ship d6111c6. Nothing assigned yet.

## Findings
- **Most of the waterfall already exists one level down.** Reports already stop at the building in-tray; review is one box and one button; a reviewer agent can already work an in-tray (policy `reviewer`, `maybeReview`); the manager is already the only conversational surface. What is missing is the top tier: a Town Hall in-tray, rollups, the manager actually reviewing, and the 1:1 (a message to the manager still becomes an assignment plus a report).
- **The budgets design survives whole, with its human surface moved.** Goal, grants with human-observable key results, proposals Mitchell funds/counters/rejects, 50% checkpoint, lanes and gate, exploration allowance all stay. Dropped: the board's fund/checkpoint buttons and the amber map dot; those decisions move to the Town Hall in-tray. Steps 1a–c (schema, Grants service, REST, board route) are built; steps 2–5 are re-sequenced into the build order.
- **The design in one line each:** review policy `manager` (the manager agent works the building in-tray in a review session, with four escalation criteria: goal/KR change, money outside a grant, real-world action, something only a human can give); rollups are reports tagged `rollup` whose provenance lists the reports they cover, so drill-down is just the links; a Town Hall in-tray place lists pending rollups plus proposed/countered/checkpoint grants with the budgets design's buttons; the manager's 1:1 is a meeting of kind `one-on-one` run as a host session with streaming input, decisions become assignments, no report.
- **Build order with owners:** 1 core (policy, rollups, in-tray query) Pix; 2 runtime (manager review sessions, rollup trigger) Root; 3 web Town Hall in-tray Lena; 4 the 1:1 Root, can start now; 5 budgets steps 2+4 Pix; 6 board as the residents' key-results view Lena; 7 Workshop pilot Pix. Steps 1–4 are about one Workshop desk session each (median ~1 M tokens, range 0.2–10 M). Sage is not needed.
- **Open:** the four budgets questions (exploration size, directed work, who funds, reservations) stay open until step 5. Kelly's meetings research (town hall decision 3) feeds steps 5 and 7.

## What I need from you
Reply "go" to the build order in [dc_g9d74v8kdb](../../article/2026-10/2026-10-24-design-note-the-waterfall-goal-directed-budgets-re-d74v8kdb.md) §5 (or say what to drop), and I assign steps 1–4 to Pix, Root and Lena.
