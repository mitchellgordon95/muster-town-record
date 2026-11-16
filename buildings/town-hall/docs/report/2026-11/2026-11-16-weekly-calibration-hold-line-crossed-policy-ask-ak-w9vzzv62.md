---
id: "dc_t8w9vzzv62"
type: "report"
state: "building"
title: "Weekly calibration: hold line crossed, policy ask ak_r31emiv274 filed"
authorId: "ag_lywy3igvel"
authorKind: "agent"
buildingId: "town-hall"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "pending"
sessionId: "se_2hconh5m0m"
assignmentId: "as_b7szosmzzj"
costUsd: 0.65733505
tokens: 32867
turns: 6
createdAt: "2026-11-16T04:06:57.546Z"
updatedAt: "2026-11-16T04:06:57.546Z"
---
## What I did
Read the calibration data, checked the board (nothing new that bears on it), and filed one policy ask with `calibrate`: ak_r31emiv274, branches Adopt / Keep as is. I changed nothing in the step-size table.

## Findings
- Crossed: hold share. 35 of 51 grants closed in the last 14 days held at a gate before closing (69%, line 25%).
- Not crossed: spend per size (S 1.02× over 2 steps, M 0.99× over 14 steps, L 0.64× over 2 steps, all under the 30-step threshold except none; M is the only size with meaningful data). Adjust asks 13 per 32 funded grants (0.41, line 0.5).
- Town's proposed change: require every L step to be split in two. Filed as the ask's rule.
- My recommendation on the card: Keep as is. Only 2 L steps completed in 30 days and both underspent, so there is no evidence that L steps cause the holds. The hold share will be read again at the next weekly run.

## What I need from you
Decide ak_r31emiv274 in the Town Hall in-tray (Adopt or Keep as is).
