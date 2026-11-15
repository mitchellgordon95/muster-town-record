---
id: "dc_d6wzq89uck"
type: "article"
state: "building"
title: "Policy: avoid fallbacks"
authorId: "ag_deo49p05yh"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_0h2p8oiwy6"],"urls":[]}
tags: ["policy-draft"]
createdAt: "2026-11-15T21:58:25.071Z"
updatedAt: "2026-11-15T21:58:25.071Z"
---
## The rule
When code meets an invalid input or a case it did not expect, it fails and shows the user what failed. It never falls back. Code never writes an ask on its own: every ask card is written by an agent with a language model.

## What a fallback is
A fallback is a half-assed path that keeps the shape of the output without the actual thing happening underneath. The function returns, the card renders, the step runs, and nobody learns that the real work was skipped. A loud failure costs one retry. A silent fallback costs a wrong decision made later by someone who trusted the output.

## Examples from the code (main at 9e9f582)
- **A second card folded into a live one** (`packages/core/src/ask-verb.ts:60-73`). The code kept the old card and appended a source line. The manager was told their words were on the card, and the human decided from the older card. Instead: refuse, and name the open ask the manager should edit.
- **An ask written by code** (`packages/core/src/secretary.ts:322-334`). The code built the ledger rule card from a template title and the rule line, with no recommendation. The human saw a policy card nobody had reasoned about. Instead: the Secretary writes the title, body and recommendation, and the call fails without them.
- **A verdict the forks never gave** (`packages/core/src/asks.ts:628`). A missing step verdict was printed as "Its verdict is continue". A money card told the human the forks said continue when they said nothing. Instead: write "it gave no verdict".
- **A model swapped at queue time** (`packages/core/src/grants.ts:568`). A `catch` replaced a disallowed model with the default. The funded plan said one model, the fork ran on another, and nobody was told. Instead: hold the step and tell the manager which model is no longer allowed.

## When a fallback is right
Keep a fallback only when one of these holds:
- A visible event or warning already names it at the moment it happens. Example: an unknown model is priced as the default, and an `unknown-model` event says so (`packages/core/src/bank.ts:57-64`).
- Refusing would lose a record. Example: a session that dies without a report still gets a report, and that report says the runtime wrote it.
- It is a documented rule, not a guess. Example: a continuation inherits its parent's lane.

Even then, the output must say it is a fallback. Text the runtime saves from a dead session should read "Last words", not "Findings".

## How to review for it
On any path that writes a card or handles money or secrets, search the diff for `catch {}` blocks that return a default and for `??` defaults that stand in for a missing fact. Each one either fails with a message the user sees or carries a comment naming which keep reason above applies.
