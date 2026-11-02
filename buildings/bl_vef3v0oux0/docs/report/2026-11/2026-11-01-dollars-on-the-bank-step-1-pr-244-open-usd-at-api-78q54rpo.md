---
id: "dc_og78q54rpo"
type: "report"
state: "building"
title: "Dollars on the Bank step 1: PR #244 open (usd at API list price on /api/finance and /spend, Overview + Spending); parked on CI"
authorId: "ag_ic2ayaetm6"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "continue"
decisionNote: "Keep the plan. One addition: PR #245 (Nell 1, adjusted-token mix, directed by Mitchell) touches core finance.ts, the finance routes, check:finance and the Tokens tab too, so one of #244/#245 will merge second. Before `gh pr ready`, run `gh pr view 244 --json mergeable,mergeStateStatus`; if it is CONFLICTING, merge origin/main into the branch, resolve (keep both the usd block and the mix), rerun npm run check --fast, push, and park again on {pr: 244}. A CONFLICTING PR gets no CI, so never park on it unresolved. After the merge, say the merged sha in the report; step 2 (as_rv1tk0dogj) starts by itself when this chain finishes."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-01T02:15:31.579Z"
sessionId: "se_ubkhs9wgcm"
assignmentId: "as_el2651coa4"
costUsd: 2.686334
tokens: 134317
turns: 47
createdAt: "2026-11-01T02:14:41.627Z"
updatedAt: "2026-11-01T02:15:31.579Z"
---
## What I did
I built step 1 of gr_gmzli3f96j on a fresh branch off main af85f2a and opened draft PR https://github.com/mitchellgordon95/muster-town/pull/244 (commit 7e8a244). It is display only: no migration, nothing stored or charged, and the Bank stays read-only. Typecheck is green. Tests: core 610/610 (includes the new `finance-usd.test.ts`), server 254/254, web 216/216 (was 208, so 8 new tests).

## Findings
- **How `usd.used` is built (core finance.ts):** Σ over all sessions of each session's booked tokens × the list output price of the model it is booked in (`bankModelOf`). Opus-booked sessions are priced at $20/M; pre-076 Fable sessions at $50/M. Then add (used − Σ session tokens) × $20/M. That difference equals spend's unattributed − weight mismatch − not funded, so /spend's `usd.used` is the same formula and both endpoints agree to the cent. A test runs both endpoints on one seeded world and checks they match.
- **Left, burn and inflow:** converted at $20/M.
- **/spend:** every row carries `usd`. There is a top-level `usd {used, sessionsTotal, unattributed, weightMismatch, notFunded}` and a `usdSumCheck`. The check passes when the top-level rows' dollars (each rounded to the cent) are within $0.01 of `usd.used`, or within half a cent per row when there are more than two rows. That allowance covers rounding only.
- **Web:**
  - The Overview's "Next 30 days" gains "Used so far" and "Left" rows. Used, Left, Burn and Coming in each read "≈ $X".
  - The Tokens tab shows "≈ $X" after Used and Left.
  - On Spending, each top-level row has a $ column and there is a ✓ line for the dollars. Child rows have no dollars.
  - One footnote: "Dollars are at API list price; a subscription pays a flat fee instead."
  - There is a new Terms entry.
  - Web types make `usd` optional, so the page renders without dollars against a server running older code.
- **check:finance gains three checks:** the two `usd.used` agree within $0.01; `usdSumCheck.ok`; the building rows' dollars sum to `usd.sessionsTotal`. The script cannot recompute Σ sessions' list cost itself, because no public endpoint lists sessions with their model. Until the PR is live these three checks fail against muster.town.
- **Dollars I could work out from live tokens at $20/M** (live 7ca64bc, read 2026-11-01T02:12:00Z; I did not run a local server with real data):
  - left 7,197,706 tokens ≈ $143.95
  - burn 10,327,183 tokens/day ≈ $206.54/day
  - inflow 11,500,000 tokens/day = $230.00/day
  - used 81,123,689 tokens is ≥ $1,622.47 at a flat $20/M. The real `usd.used` will be higher because the pre-076 Fable sessions are priced at $50/M. I can only read that figure once the PR is deployed.
- **Next session plan:** If CI is green, run `gh pr ready 244`, check the PR is still mergeable, merge, call `redeploy` and say which sha should be live. Then rewrite [dc_tkzoy81p4b](../../wiki/2026-10/2026-10-29-the-three-finance-endpoints-their-sum-checks-and-l-zoy81p4b.md) (the usd block, the three new checks, live after the deploy) and [dc_nb3743g7f6](../../wiki/2026-10/2026-10-29-the-bank-page-bankpanel-bankfinance-its-tests-and-3743g7f6.md) (the ≈ $ rows, the Spending $ column, the footnote). Report the merged sha. On the first session after the deploy, read the live usd numbers and run check:finance.

## What I need from you
Nothing needed.
