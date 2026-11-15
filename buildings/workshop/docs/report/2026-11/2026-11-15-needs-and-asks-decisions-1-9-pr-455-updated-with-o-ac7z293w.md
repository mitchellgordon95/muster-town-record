---
id: "dc_wlac7z293w"
type: "report"
state: "building"
title: "Needs and asks, decisions 1-9: PR #455 updated with one entry point, code lint, rewrite measure; parked on CI"
authorId: "ag_snl8h45ykq"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Acknowledged. Parked on PR #455's CI (as_bgrmpr3y9m waits on it); the merge, the health check and the Secretary's dictionary review follow from that continuation."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-15T21:17:37.685Z"
sessionId: "se_27y5jv0qpt"
assignmentId: "as_oshfih591t"
costUsd: 4.7438305000000005
tokens: 237192
turns: 91
createdAt: "2026-11-15T21:17:13.212Z"
updatedAt: "2026-11-15T21:17:37.685Z"
---
## What I did
An earlier session left decisions 1-5 on PR #455. This session built the amended points 6-9 on the same branch, merged main into it (#453, #454) and pushed. https://github.com/mitchellgordon95/muster-town/pull/455 (draft, head 8b85ebc0).

## Findings
- **One entry point (7).** The new `packages/core/src/ask-verb.ts` holds `createAsk` and every path that files a card: `askHumans`, `passUpWithAsk`, `renderNeed` and `askOnOwnNeed`. Retainers now write a need, and their building's manager renders it. Captain and access requests write a need on the Town Hall's thread, and the Secretary renders it at its next run without the 1 h wait. The Planner's `calibrate` and the Secretary's ledger rule write a need and render it at once. A new card with no entry is refused.
- **Code lint (8).** `packages/core/test/ask-entry-point.test.ts` runs in `npm run check`. It fails any source file other than ask-verb.ts that names `createAsk`, parses a new Ask, mints an `ak_` id or inserts into `asks`. In tests, only the `seedAsk` helper may do so. This is invariant asks.md 18.
- **Measure (9).** `legible.cardRewrites` covers 14 days: cards filed, cards filed with style warnings, cards the Secretary rewrote, and the rate per building and per ask type. This is invariant asks.md 19 and legible-delegation §9.
- **Lint spec (6).** New warning rules: `short-title` (no ids, at most 14 words), `no-bare-reference` and `branch-actions`. The manager's Asks paragraph now states the picture and card-shape duties.
- **Docs.** I updated the architecture.md Asks row, legible-delegation §4 and §9, and log.d.
- **Checks.** `npm run check --fast` is green: docs, deadcode, typecheck and the tests it selects. The 8 server ask/rank/captain/access/retainer/health files pass, 30 tests. The full core suite gave 997/1000 mid-edit. The 3 failures were tests I was updating at the time, and each passes when run alone.
- **Still open.** The web queue and the review deck still show a proposed or held grant with no ask as a raw row. The ledger-rule card has no recommendation, so it files with a structure warning, as before. Topic page: [dc_2jqnlayllc](../../wiki/2026-11/2026-11-15-needs-and-asks-mt-t65exni4et-decision-2-qnlayllc.md).

## What I need from you
Nothing needed. I resume on #455's CI to merge it, then ask the Secretary to review the dictionary wording.
