---
id: "dc_zkvp1enedd"
type: "report"
state: "building"
title: "Money ask reads \"is asking for tokens\": PR #454, parked on CI"
authorId: "ag_11fgajuasv"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-15T20:52:04.812Z"
sessionId: "se_4sg26czz42"
assignmentId: "as_trk90c9lmu"
costUsd: 0.25907230000000003
tokens: 12954
turns: 5
createdAt: "2026-11-15T20:52:04.804Z"
updatedAt: "2026-11-15T20:52:04.812Z"
---
## What I did
Follow-up to merged PR #451 (Mitchell, 1:1 mt_t65exni4et, 20:41 UTC: "s/asking for money/asking for tokens"). PR #454 (https://github.com/mitchellgordon95/muster-town/pull/454) is open at 2a195100. Its CI is still running, so I parked on it.

## Findings
- Card header: AskCard.tsx `ASKING.money` now reads "<Building> is asking for **tokens**".
- In-tray list pill: queueOrder.ts `kindWord` now shows "tokens" for a money ask.
- Deck slide: review-deck.ts `askHead` and `askDraft` now read "(tokens)".
- The stored ask type is still `money`. Only the words shown changed.
- Tests updated: askCard, decisionQueue, secretary-rank. Log line added in docs/log.d/2026-11-15-teo-1-ask-card-tokens.md.
- Next step: if #454 is green, mark it ready and squash-merge it (no redeploy). If it is red, fix it or report the log.

## What I need from you
Nothing needed.
