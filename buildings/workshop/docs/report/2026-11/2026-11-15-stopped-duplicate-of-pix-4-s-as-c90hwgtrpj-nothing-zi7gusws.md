---
id: "dc_zwzi7gusws"
type: "report"
state: "building"
title: "Stopped: duplicate of Pix 4's as_c90hwgtrpj; nothing changed"
authorId: "ag_ffxv5aulcr"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Settled by the town: the request is done."
decidedBy: "system"
decidedAt: "2026-11-15T21:27:09.992Z"
sessionId: "se_814wdc0f3j"
assignmentId: "as_wzm292g3oe"
costUsd: 0.36836179999999996
tokens: 18418
turns: 2
createdAt: "2026-11-15T21:27:09.981Z"
updatedAt: "2026-11-15T21:27:09.992Z"
---
## What I did
I read the current fold path (`packages/core/src/ask-verb.ts` createAsk, lines 54-90; it moved out of asks.ts in PR #455) and listed where `ask.sources` is used. Pix stopped me because this duplicates as_c90hwgtrpj. I changed no code and opened no branch commits or PR.

## Findings
In case Pix 4 finds it useful, here is where `ask.sources` is read today (from grep on main b80f73cd):
- core/src/review-entry.ts:100
- core/src/secretary.ts:451 and :623
- core/src/review-deck.ts:275, :328 and :344
- core/src/asks.ts:541
- web/src/panels/AskCard.tsx:171-174
- web/src/panels/queueOrder.ts:39
- web/src/mock/fixture.ts

The `folded` status and `foldedInto` already exist in the schema and in 097_asks.sql, but nothing sets them yet.

## What I need from you
Nothing needed.
