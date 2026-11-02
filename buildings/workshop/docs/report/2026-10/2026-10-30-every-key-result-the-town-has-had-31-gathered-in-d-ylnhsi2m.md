---
id: "dc_vbylnhsi2m"
type: "report"
state: "building"
title: "Every key result the town has had (31) gathered in dc_io1ry1ryjz for Mitchell's standing-goal sort"
authorId: "ag_mylcp133yw"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_io1ry1ryjz","mt_kh0zaqui0w","dc_0xqyrevla1"],"urls":["https://muster.town/api/kpis","https://muster.town/api/events"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "KR inventory dc_io1ry1ryjz presented to Mitchell in 1:1 mt_kh0zaqui0w."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-30T20:25:00.471Z"
sessionId: "se_cjb9ul89zu"
assignmentId: "as_q2oej9leub"
costUsd: 1.2788672
tokens: 63943
turns: 37
createdAt: "2026-10-30T20:24:44.947Z"
updatedAt: "2026-10-30T20:25:00.471Z"
---
## What I did
Read-only; no code was changed. I pulled every building's objectives and key results (GET /api/kpis), all grants (GET /api/buildings/:id/grants for each building, including the Town Hall) and the whole event log (62,291 events, 2026-10-20 to 2026-10-30 20:23Z). From those I built one table per building and published it as a note in the Workshop filing cabinet: **[dc_io1ry1ryjz](../../note/2026-10/2026-10-30-every-key-result-the-town-has-had-31-for-sorting-i-1ry1ryjz.md)** ("Every key result the town has had (31), for sorting into standing goals"). I also updated the topic page [dc_0xqyrevla1](../../wiki/2026-10/2026-10-30-town-level-goal-tree-design-qyrevla1.md).

## Findings
- **The 31 key results are the town's full history.** The event log has 31 `kr.created` events and 0 `kr.deleted`. The first key result was written 2026-10-26 15:42Z; before that no grant named one (gr_jqsqra0dlx, rejected 2026-10-25, had none).
- **Status today:** 12 met (these are the 12 "archived"), 2 claimed and waiting on Mitchell's met/missed (#12 Prod monitoring kr_iwj8m0461p, #25 Code fast check kr_939kp3vjxc), 6 on-track, 11 not-started, 0 missed.
- **By building:** Workshop 5, Onboarding 6, Prod 8, Bank Transparency 4, Code Legibility 8. UI / UX has never had a key result.
- **Objectives:** 18 of the 31 key results never got an objective (Unsorted). There are 6 objectives, all 2026-Q4, none ever deleted: Workshop 3, Prod 2, Code 1. They are listed in their own section at the end, with a "Standing goal?" column.
- **Grants:** 27 in total: 3 funded, 13 closed done, 6 cut, 5 rejected. Each grant cell shows spent / granted adjusted tokens. Four cut grants spent more than they were granted (e.g. gr_jh0lu0w6yj 1,166,710 / 1,100,000).
- **Status lag:** three key results still read "on-track" even though their only grant was cut: #3 kr_2qg0ayfs1j, #6 kr_z0mj5teeu7 and #7 kr_1rpq0738sw. The note points this out so the status isn't taken at face value.
- **What each row has:** number, objective, the full key result text with its id, status, grants, when it was written and by whom, when it closed, and a blank "Standing goal?" column. Four key results were reworded after they were written; their first wording is shown under the current text.
- **The note restates the shape agreed in mt_kh0zaqui0w:** one root goal (the town goal), Fund / Join / Trust as placeholder children, unbounded depth, key results always dated leaves, no KPIs yet.

## What I need from you
Pix: present [dc_io1ry1ryjz](../../note/2026-10/2026-10-30-every-key-result-the-town-has-had-31-for-sorting-i-1ry1ryjz.md) to Mitchell so he can fill in the "Standing goal?" column.
