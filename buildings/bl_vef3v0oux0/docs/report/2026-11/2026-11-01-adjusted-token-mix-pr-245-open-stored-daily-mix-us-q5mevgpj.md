---
id: "dc_0vq5mevgpj"
type: "report"
state: "building"
title: "Adjusted-token mix: PR #245 open (stored daily mix, used for bare numbers, shown on Tokens & sources); parked on CI"
authorId: "ag_4xzwcmdmhn"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "continue"
decisionNote: "Keep the plan on dc_ydgrv1arc3. One addition: PR #244 (Nell 2, dollars at API list price on /api/finance, /spend, Overview, Spending and the Tokens tab) touches core finance.ts, the finance routes, check:finance and BankFinance.tsx too, so one of #244/#245 will merge second. Before `gh pr ready`, run `gh pr view 245 --json mergeable,mergeStateStatus`; if it is CONFLICTING, merge origin/main into the branch, resolve (keep both the mix and the usd block), rerun npm run check --fast, push, and park again on {pr: 245}. A CONFLICTING PR gets no CI, so never park on it unresolved. Say the merged sha in the report and queue the redeploy with the tool."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-01T02:15:35.325Z"
sessionId: "se_baml4ivaog"
assignmentId: "as_hdtgd07jzi"
costUsd: 2.8102833000000014
tokens: 140514
turns: 58
createdAt: "2026-11-01T02:15:03.522Z"
updatedAt: "2026-11-01T02:15:35.325Z"
---
## What I did
Checked main first. Core's Bank refactor has landed and builds (PR #231 4752cf1: every charge is booked in Opus 5.5 output tokens). Then I built the mix on top of it and opened draft **PR #245** (https://github.com/mitchellgordon95/muster-town/pull/245). `npm run check --fast` passes locally: typecheck, plus core 593, server 202, runtime 249 and web 175 tests. The PR is mergeable. I've parked until its CI finishes.

## Findings
- **The formula is the same before and after, and it's exact.** adj. tokens = output + 0.2 × input + 0.01 × cache read + 0.25 × cache write (5 min) + 0.4 × cache write (1 h). Each weight is that kind's Opus 5.5 list price divided by its $20/MTok output price. Other models are priced at their own list price and converted at $20/MTok. Every session's real counters are still priced this way, so the mix never replaces these weights.
- **The one hardcoded estimate before this PR** was the step-1 back-fill: 1 adj. token = 30 raw tokens (24 on Fable), split into output plus cache read. It was used whenever the Bank had only a bare adjusted number: the counters behind a Bank input's credits, bare-number charges and usage records, and bare-number draws.
- **What PR #245 does:**
  - It computes one global mix (`core/token-mix.ts`) from the five counters summed over ended sessions in the last 7 full UTC days. Back-filled sessions are left out. The mix holds raw share and cost share per kind, raw tokens per adj. token, the formula, the window and computedAt.
  - It's stored in the DB's `meta` table under `tokenMix`. That needed no migration, so there's no migration-number clash to worry about.
  - The first read back-fills it from the existing logs. The runtime tick (the same hook the drift job uses) recomputes it once per UTC day and posts a `bank.mix` event.
  - The bare-number paths now split by the mix instead of the fixed 30.
  - The old `splitRaw` is kept for history and for desks that post only a raw total, so back-filled rows are still recognised.
  - `GET /api/finance` and `GET /api/bank` both carry `mix`.
  - `check:finance` gains 6 mix checks: the counts sum to the raw total, it prices back to its adj. tokens (±1), raw-per-adj. is consistent, both share sets sum to 1, the two endpoints carry the same record, and it was computed under 26 h ago.
- **On the page:** the Tokens & sources tab, under the Tokens sum check, reads "1 adj. token ≈ R raw tokens: x% input, y% cache read, z% cache write, w% output (from the last 7 days of usage, N sessions, updated daily; last …)", with the formula and cost shares on a sub-line. The fixed "≈ 30 raw tokens" wording in the intro, the Terms block and the adj. token hover now points to that line instead.
- **Not done yet:** the live percentages and the cropped picture. Both need #245 deployed, and the continuation will do them. Teo isn't told yet; the continuation will tell them.
- The plan for the next session is on topic page [dc_ydgrv1arc3](../../wiki/2026-11/2026-11-01-adjusted-token-mix-what-1-adj-token-is-made-of-grv1arc3.md).

## What I need from you
Nothing needed.
