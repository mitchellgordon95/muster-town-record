---
id: "dc_spp17yejo1"
type: "report"
state: "building"
title: "Bank UX pass: grant gr_567tikzitl still awaits Mitchell; build plan, before-measurements and pictures filed so step 1 starts the moment it is funded"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_zuh4oien9g","dc_8n3on7i7l6","dc_we5nqevv40"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Groundwork done; grant gr_567tikzitl awaits Mitchell. Teo's chest/fountain conventions (ms_gigclmdvc7) folded into the topic page so step 2 starts from them."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-03T22:53:44.957Z"
sessionId: "se_kv17jyeh8b"
assignmentId: "as_m9x23d0ji9"
costUsd: 2.9838564499999998
tokens: 149193
turns: 35
createdAt: "2026-11-03T22:53:20.816Z"
updatedAt: "2026-11-03T22:53:44.957Z"
---
## What I did
The 1:1 decision runs the Bank UX pass as grant gr_567tikzitl, and that grant is still proposed (checked GET /api/grants/gr_567tikzitl: status proposed, ask 1,200,000, model estimate 350k–800k). No code until Mitchell funds or counters it, so this session did the groundwork: measured every Bank tab live, shot the two before-pictures I lacked, filed a file-level build plan ([dc_8n3on7i7l6](../../note/2026-11/2026-11-03-bank-sheet-build-plan-gr-567tikzitl-file-level-inv-3on7i7l6.md)) and a topic page ([dc_we5nqevv40](../../wiki/2026-11/2026-11-03-bank-sheet-rebuild-gr-567tikzitl-plan-and-state-5nqevv40.md)) a fork starts from, and asked Teo (ms_5elv3fcnl9, queued to Teo as as_jqloithobc) about the chest sprite and the fountain removal. Nothing on the queue.

## Findings
Before, at live 1826430, 1400×900 signed out (panel body 760 px):

| tab | scroll px | screens | prose blocks | words |
|---|---|---|---|---|
| Overview | 1,605 | 2.1 | 4 | 411 |
| Tokens & sources | 3,832 | 5.0 | 5 | 1,098 |
| Free tokens | 1,807 | 2.4 | 2 | 542 |
| Spending | 7,258 | 9.6 | 6 | 3,631 |
| Hosting | 977 | 1.3 | 3 | 304 |

- Donate starts 1,397 px down Overview (mf_lp13m3tjub). Bank inputs: 18 rows, 15 cancelled, 1,288 px tall (mf_tihjpsddmr). Sources: 56 rows. Spending: 1,550 rows, Spend by goal alone 5,449 px.
- The sheet shell is reusable as planned: GoalTreePanel.tsx 41-120 (createPortal, ge-* classes, Esc only with no side panel), panelResize GeDivider, styles.css 800-871, mounted in app.tsx 226-235/318. Every opener (HUD $, map stations, #/bank, meeting attach, planning panel) passes PanelRef kind "bank", so the sheet replaces the side panel without touching them.
- The room is schema BANK_FIXTURES (index.ts 2143-2190): the chest takes the fountain's two cells (2,5)-(3,5), so walkability and roads are unchanged; the fountain sprite (sprites.ts 264) becomes a chest.
- Five PRs, each shippable with pictures after it: 1 sheet shell (kr_9xozv5d8gh); 2 Donate tab + chest + fountain gone + Balance "Free for exploration" line (kr_00lym2zmif, kr_lq1qmywinq, one PR since both edit BANK_FIXTURES); 3 one active-only Inputs table with "Show N cancelled" and row credits in the sidebar (kr_y7derda40x); 4 Spending drill-down over the same spend tree (kr_trhi5frg4k); 5 live verification. Rough sizes 150-250k, 150-250k, 100-150k, 150-250k, ~100k: 650k–1M, inside the 1.2M ask. Countered at 600k: steps 1-3, checkpoint before Spending. No endpoint changes, so check:finance stays the proof.

## What I need from you
Nothing needed: the funding decision on gr_567tikzitl is already in the Town Hall in-tray and wakes me with its own assignment.
