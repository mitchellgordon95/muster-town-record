---
id: "dc_mbmlzp4tsf"
type: "report"
state: "building"
title: "Draft \"Policy: avoid fallbacks\" filed as dc_d6wzq89uck; Secretary told"
authorId: "ag_deo49p05yh"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Draft dc_d6wzq89uck filed as an article (agents can't write type policy); the Secretary has the id for the ledger ask. Nothing further queued."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-15T21:58:45.866Z"
sessionId: "se_3xcrottnu4"
assignmentId: "as_wom9ekzqqs"
costUsd: 0.4163988
tokens: 20820
turns: 9
createdAt: "2026-11-15T21:58:37.246Z"
updatedAt: "2026-11-15T21:58:45.866Z"
---
## What I did
I read the audit, [dc_0h2p8oiwy6](2026-11-15-fallback-audit-20-fallbacks-ranked-by-harm-10-to-f-2p8oiwy6.md). I checked the cited lines at main 9e9f582 and wrote the draft rule as [dc_d6wzq89uck](../../article/2026-11/2026-11-15-policy-avoid-fallbacks-wzq89uck.md). I told the Secretary the doc id in ms_tya8iz3u5z and updated the topic page [dc_fu5unwj1kr](../../wiki/2026-11/2026-11-15-fallback-audit-decision-5-5unwj1kr.md). I made no code changes and did not file the policy ask myself.

## Findings
- **The draft is [dc_d6wzq89uck](../../article/2026-11/2026-11-15-policy-avoid-fallbacks-wzq89uck.md), titled "Policy: avoid fallbacks".** It is filed as an article, not type policy, because the town refuses `write` type policy from agents. Only a human adds to the policy ledger, through a policy ask.
- **What the draft says:**
  - The rule, in two sentences.
  - What a fallback is, using Mitchell's phrase "keeps the shape of the output without the actual thing happening underneath".
  - Four examples, each with what the code did, what the user saw and what it should do instead:
    - the ask fold at ask-verb.ts:60-73
    - the code-written ledger ask at secretary.ts:322-334
    - the "verdict is continue" default at asks.ts:628
    - the model swapped inside a catch at grants.ts:568
  - When a fallback is right, so the rule is not absolute. The draft names three cases:
    - a visible event already names it (bank.ts:57-64)
    - refusing would lose a record
    - a documented rule covers it
  - How to review for it: on card, money and secret paths, look for silent `catch {}` blocks and `??` defaults.

## What I need from you
Nothing needed.
