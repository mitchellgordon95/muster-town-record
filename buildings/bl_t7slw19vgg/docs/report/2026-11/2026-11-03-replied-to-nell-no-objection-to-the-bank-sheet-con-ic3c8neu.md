---
id: "dc_15ic3c8neu"
type: "report"
state: "building"
title: "Replied to Nell: no objection to the Bank sheet; conventions for the chest fixture"
authorId: "ag_s1kuuuo54b"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-03T22:50:00.577Z"
sessionId: "se_02wei9wxb2"
assignmentId: "as_jqloithobc"
costUsd: 0.39999
tokens: 20000
turns: 8
createdAt: "2026-11-03T22:49:45.893Z"
updatedAt: "2026-11-03T22:50:00.577Z"
---
## What I did
I read BANK_FIXTURES and TILE (schema index.ts) and the Bank sprites (web map/sprites.ts, world.ts). Then I replied to Nell (ms_gigclmdvc7) about the Bank-as-sheet plan (gr_567tikzitl, notes [dc_zuh4oien9g](../../../../bl_vef3v0oux0/docs/meeting-notes/2026-11/2026-11-03-1-1-mitchell-and-nell-notes-h4oien9g.md)).

## Findings
- No objection. The goal-editor shell, copied to bank-* classes, is the right choice.
- The chest takes the fountain's slot (cells {2,5},{3,5}, stand {2,6}), below the ledger desk, so money coming in stays on the left.
- The chest gets a new tile id, TILE.BANK_CHEST = 35, and BANK_FOUNTAIN 23 is retired instead of reused.
- The sprite is two halves in the drawBankLedger pattern (n:{l,r}), in the room's wood and gold palette.
- `bank:free` stays as an alias for Balance, so old links don't break.
- Making Donate the first tab changes BANK_TABS and the order pinned in finance.test.tsx.
- Per-goal free tokens are already shown in the goal editor, so dropping the Free tokens tab loses nothing.

## What I need from you
Nothing needed.
