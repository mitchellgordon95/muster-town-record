---
id: "dc_ke6lr93jnx"
type: "report"
state: "building"
title: "077a0bd is live: the in-tray header shows a separate ⚑ flag count"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved; plant-a-flag fully live (077a0bd on db3534a). Closed."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-26T23:31:52.947Z"
sessionId: "se_qng0tzpipf"
assignmentId: "as_w5j31wdfvm"
costUsd: 0.3039821
tokens: 12360
turns: 11
createdAt: "2026-10-26T23:31:44.327Z"
updatedAt: "2026-10-26T23:31:52.947Z"
---
## What I did
Checked the live server's commit and grepped the live map bundle for the in-tray flag pill from 077a0bd (report [dc_fcapf2xmbr](2026-10-26-plant-a-flag-was-already-shipped-added-a-separate-apf2xmbr.md)).

## Findings
- GET /api/health reports commit db3534a (2026-10-26T23:31Z). `git merge-base --is-ancestor 077a0bd db3534a` succeeds, so 077a0bd is live.
- The live bundle /workshop/assets/main-kjPQINdR.js (265 KB) has the pill: `title:"Flags humans planted here, waiting for the manager to delegate",children:["⚑ ",k]`. It also has `filter(b=>b.type==="flag").length`, and that number is subtracted from the plain in-tray count, so flags are counted only once, in their own pill. A later commit added access requests to that count; the flag subtraction is unchanged.
- No flags were waiting at check time (Workshop in-tray: 2 items, 0 flags; Town Hall: 1 item, 0 flags), so I haven't seen the pill drawn on screen yet.
- How Mitchell plants a flag: press F on the map, pick the building, type the note, then click Plant. The flag shows up in that manager's in-tray with its own ⚑ n count.
- Plant a flag is fully shipped: core 7810e8c, web 9b20fad, d60fdaf, 077a0bd. This assignment is done.

## What I need from you
Nothing needed.
