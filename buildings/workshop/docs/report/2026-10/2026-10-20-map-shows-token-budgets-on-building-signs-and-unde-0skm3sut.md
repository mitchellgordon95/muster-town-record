---
id: "dc_mc0skm3sut"
type: "report"
state: "building"
title: "Map shows token budgets on building signs and under residents' names (PR #31)"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":["https://github.com/mitchellgordon95/agent-town/pull/31"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "merge"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T04:22:04.655Z"
sessionId: "se_bfl7qulx82"
assignmentId: "as_lkt9mylp3c"
costUsd: 1.1830908999999998
tokens: 81672
turns: 40
createdAt: "2026-10-20T04:18:26.853Z"
updatedAt: "2026-10-20T04:22:04.655Z"
---
## What I did
Added token budgets to the map overlay. Building signs now show the building's tokens used and left. Each resident's name tag shows tokens used today and what's left of their daily allowance. Draft PR: https://github.com/mitchellgordon95/agent-town/pull/31

## Findings
- **Building signs** get a third line, e.g. "3.4M used · 47M left" for Carbon Cycle Lab in the mock (50M house allocation). Buildings that never had an allocation, like Town Hall, show no line.
- **Name tags** get a small line, e.g. "Noor · 412k today · 1.6M left". The "left" figure is `dailyTokensPerAgent − spentTokensToday` and never goes below 0. Only residents get it, not services or humans.
- **Server side:** snapshot and WS building messages now carry an optional derived `budget` with `allocatedTokens`, `spentTokens` and `remainingTokens`. A new `Budget.of()` computes it, and `summary()` and `remaining()` now reuse it. The building is resent on every charge and donation, so signs update live. Resident spend was already streamed through agent updates. `docs/architecture.md` and `docs/log.md` are updated.
- **Verified:**
  - `npm run typecheck` passes and `npm test` passes in every package.
  - A new core test checks that the snapshot carries the budget and that a charge resends it.
  - A new web test covers how the two lines are formatted.
  - In the mock UI in headless Chromium, the sign and name tags render, and the sign ticks up as agents work.
- **Limitation:** Town Hall residents (e.g. Moss, Wren) also show a daily-allowance line, even though Town Hall has no allocation. Their spend is still recorded against their daily allowance, so the number is accurate.

## What I need from you
Review and merge PR #31.

## Reply from Mitchell (2026-10-20 00:22)

merge

