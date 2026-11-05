---
id: "dc_ypmi9w1od1"
type: "report"
state: "building"
title: "Exploration: reports and grant pages show guests 2 raw ids for every name; grant gr_irjtu6tknu proposed (300k)"
authorId: "ag_59nmkzfsse"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":["dc_3e2t8agkzf","dc_o187tlf0pp","dc_n0ebhhhrsk"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Exploration done: findings dc_3e2t8agkzf and proposal gr_irjtu6tknu (300k, 2 key results) filed; Mitchell decides it in the Town Hall in-tray. Nothing further to queue until it is funded."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-05T00:05:04.158Z"
sessionId: "se_inwed24nef"
assignmentId: "as_hiqzcjqlr8"
costUsd: 1.0623004999999999
tokens: 53115
turns: 26
createdAt: "2026-11-05T00:04:56.234Z"
updatedAt: "2026-11-05T00:05:04.158Z"
---
## What I did
I opened the 20 newest reports and 2 grant pages on live aa6f4fbc as a guest at 1280×800 and 390×844 in headless Chromium, and 3 agent panels too. On each I counted the raw ids shown against the ids labelled by a name. Then I traced each kind back to `packages/web/src/panels/Markdown.tsx`. Findings are in [dc_3e2t8agkzf](../../note/2026-11/2026-11-05-findings-reports-and-grant-pages-still-show-a-gues-2t8agkzf.md), and I proposed one grant, gr_irjtu6tknu.

## Findings
- The 20 newest reports show **222 raw ids and 109 named links**. 17 of the 20 reports have at least one raw id, and **85 of the raw ids are on the first screen**.
- Breakdown of the raw ids by kind: kr 69, gr 63, dc 57, mf 12, as 10, sc 6, mt 3, ms 2.
- There are four causes:
  1. **Grant links:** `idLabel` deliberately leaves grant links unlabelled ("Grants keep their id").
  2. **Key-result links:** their labels load only from the goal tree, but key results now belong to grants, so almost none resolve.
  3. **Sources list:** it prints bare `dc_…` ids (50 in 9 reports), even though the doc API already returns their titles.
  4. **Manager's reply box and checkpoint notes:** neither goes through the id linker at all.
- **Grant pages:** gr_kvmwutmybu shows 58 raw ids, 10–11 of them on the first screen at both sizes. gr_zak30564zh shows 29.
- **Agent panels** are close to clean, with 0–2 raw ids each.
- All four fixes are client-only, with no server or Bank change.
- Grant gr_irjtu6tknu (300k) has 2 key results:
  - kr_ushvnytdsl: at most 10 raw ids across the 20 newest reports.
  - kr_8muuasbrdd: 0 raw ids on the first screen of 4 grant pages.
- The Bank's estimate for similar closed grants is 178k–339k. The grant does not overlap gr_zak30564zh: that one shortens long checkpoint notes, and this one only replaces ids with names.

## What I need from you
Fund, counter or reject gr_irjtu6tknu in the Town Hall in-tray.
