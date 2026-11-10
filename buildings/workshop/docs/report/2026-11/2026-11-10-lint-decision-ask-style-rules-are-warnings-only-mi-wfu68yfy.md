---
id: "dc_ipwfu68yfy"
type: "report"
state: "building"
title: "Lint decision: ask style rules are warnings, only missing structure is refused (PR #412, CI pending)"
authorId: "ag_wqa7t10gqd"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Acknowledged: PR #412 (style rules are warnings, structure refused) is parked on CI; as_s9t0vysjnd merges it on green. Nothing more to queue."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-10T19:29:21.003Z"
sessionId: "se_a2b9zgvvwa"
assignmentId: "as_sbfjf35p9t"
costUsd: 1.9976806999999999
tokens: 99884
turns: 34
createdAt: "2026-11-10T19:28:59.003Z"
updatedAt: "2026-11-10T19:29:21.003Z"
---
## What I did
I built Mitchell's lint decision (1:1 mt_ewxnhs90cq, decision 5) as one PR: https://github.com/mitchellgordon95/muster-town/pull/412 (draft). Tests pass on my desk: core 905/905, web 366/366, server 304/304. Typecheck, check:docs and knip are clean too. The work is parked until CI finishes; then the continuation merges it.

## Findings
**These were refusals and are now warnings.** The card is filed, the broken rules go into one `lint` history entry that starts "warnings:", the author's answer names them, and the card gets no tag or pill:
- the style rules: sentence-length, no-ids, no-semicolons, no-parentheses, one-instruction, condition-first, no-ellipsis, dictionary
- the "X recommends …" sentence as a stand-in for the recommendation
- the soft contract fields: money claims, click permission, policy what-I-did and reversing cost

**These are still refused, every time, with no third-try escape:**
- fewer than two branches
- an empty recommendation field
- the hard contract fields: money prior decision, spent and steps; click who is parked; credential scope and fallback; meeting the question; policy the rule

A money ask still needs a grant or retainer target, as before. Other ask types still don't require a target. Making one required would refuse click or credential cards that have nothing in the town to point at, so I left that rule as it was.

**Where the code changed:**
- Applies to rollup typed asks, propose_grant's `ask` and the Planner's `calibrate` card. The new checks are in `packages/schema/src/ask.ts`: `askStructure` and `askWarnings`. `ASK_LINT_RULES` is unchanged data.
- Removed: `refuseOrFlag`, the three-tries counter, `ask.refused` events, the `lint-failed` tag and the AskCard pill. Old tags drop off when a card is rewritten.
- The prompt (prompts.ts askCardRules) now says the style rules are not refused. It adds two lines: write in the active voice, and use the dictionary's words.
- The decision is written into legible-delegation.md §12 question 4 and invariants/asks.md #8. Topic page: [dc_b4musn05et](../../wiki/2026-11/2026-11-10-ask-card-lint-decision-style-warns-structure-refus-musn05et.md).

## What I need from you
Nothing needed. The continuation merges PR #412 when CI is green.
