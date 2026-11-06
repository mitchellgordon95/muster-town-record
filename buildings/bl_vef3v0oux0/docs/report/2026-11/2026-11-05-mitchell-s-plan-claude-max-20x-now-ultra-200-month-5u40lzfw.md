---
id: "dc_qh5u40lzfw"
type: "report"
state: "building"
title: "Mitchell's plan (Claude Max 20x, now \"Ultra\", $200/month from 2026-10-25) seeded from collective.json into \"Plans paid for\" and a hosted collective's cash row never reads no plans as a gap: PR #370 in CI, admin add form exercised locally"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_aucmysyxl0","dc_a6h42ryd7k"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/370"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Parked continuation as_04vff3fqca already resumed (PR #370 CI finished): merge if green, park on deploy, verify live. Nothing more to assign."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-05T20:50:11.218Z"
sessionId: "se_a8thsigyqb"
assignmentId: "as_667a9q1xaq"
costUsd: 6.2783416999999995
tokens: 313917
turns: 68
createdAt: "2026-11-05T20:49:43.248Z"
updatedAt: "2026-11-05T20:50:11.218Z"
---
## What I did
Mitchell's word in the 1:1 mt_pr3347g2w2 (19:37 UTC): "Max 20x since like Oct 25th, $200 (renamed to ultra)". Agents hold agent tokens only (`POST /api/bank/fees` needs a user token), so I seeded the entry instead of posting it: `collectives/workshop/collective.json` gains `plans: [{label: 'Claude Max 20x (now "Ultra")', usdPerMonth: 200, from: "2026-10-25"}]` and the seed records each plan there into the Bank's "Plans paid for" on every boot unless a fee with that label and first day exists (core `Bank.seedFees`; a `bank.fee` event with `seeded: true`; never on a hosted collective). A self-hosted town spells its plan the same way.

His second point ("most hosted collectives will not have a subscription token"): `GET /api/finance` `cash` gains `hosted`; the Balance cash row's parts then read "API keys $B · hosting $C (no plans: a hosted collective runs on API keys)", the $0 case says "Nothing paid in cash in these 30 days yet." instead of pointing at Inputs, and the Inputs "Plans paid for" section says "None: a hosted collective runs on API keys, not a subscription plan." with no admin form.

I exercised the admin add form myself on a local throwaway server (`MUSTER_TOWN_RUNTIME=off`, the built web client, the seeded admin token in the browser's localStorage), with the real entry.

PR #370: https://github.com/mitchellgordon95/muster-town/pull/370 (draft, head b7e582e1 after merging main; CI run 42106749547 in progress at 20:48 UTC). `npm run check` was green on 1dcf4d0f (docs, dead code, typecheck, core 7xx + web 343 + server tests); after the merge with main the fast check ran and showed no failure. Tests added: core bank-fees (seedFees once, dedupe against a hand-added row, hosted skipped), finance-cash (`hosted`), fresh-seed (a collective.json with plans → one row at seed, still one on the next boot, none on a hosted world; the Workshop's file names its plan); web finance (hosted wording, no form). docs/bank.md and docs/log.md updated. Topic page [dc_aucmysyxl0](../../wiki/2026-11/2026-11-04-cash-cost-of-running-the-collective-gr-qggxximtru-cmysyxl0.md) rewritten.

## Findings
- **The admin add form works end to end** (never exercised before): signed in as the local admin, Bank › Inputs › "Plans paid for", filled Plan / $ per month / From and clicked Add plan. The row listed as `Claude Max 20x (now "Ultra") · $200 · 2026-10-25 · ongoing · End`; `GET /api/bank/fees` held it; the event read "Mitchell recorded a plan paid for: … $200/month from 2026-10-25".
  ![Local server, signed in as admin: Plans paid for lists Claude Max 20x (now Ultra), $200/month from 2026-10-25, ongoing, with End and the add form](/api/media/mf_p22grchmab.png)
- **The cash row prorates it as designed**: at 20:24 UTC the local row read "Paid in cash, last 30 days $112.05 = plans $79.05 · API keys $0.00 · hosting $33.00", `planRows` activeDays 11.85 (2026-10-25 00:00Z to now, of 30), $200 × 11.85 / 30 = $79.00 ± $0.05 rounding, ✓ check.
  ![Local server, signed out: Paid in cash, last 30 days $112.05 = plans $79.05 (11.85 of 30 days) + API keys $0 + hosting $33](/api/media/mf_b1ezqj79zw.png)
- **The seed is idempotent**: a fresh boot from the new collective.json seeded exactly one row (event "collective.json records a plan paid for: …"); a second boot kept one; a boot over the data dir where the form had already added the row added none (label + first day match).
- **Live today** (cd1adc86, 20:13 UTC): `GET /api/bank/fees` is `[]`, cash = plans $0 · API keys $0 · hosting $40.21, total $40.21, listUsd $3,288.13, perDollar 81.77. After #370 deploys, plans will be ≈ $80 on 2026-11-06 (12 of 30 days) rising to $200 by 2026-11-24, and "each $1 paid bought" will fall from ≈ 82 to ≈ 27 at today's list-price volume. The 2026-10-25 start is Mitchell's "since like Oct 25th", so the figure is approximate by up to a few days (≈ $7/day); an admin can move it with End + a new row if he knows the real date.
- The PR opened from a branch 12 commits behind main got no CI run until I merged main and pushed (same as #362/#364 earlier today).

## What I need from you
Nothing needed: merging #370 when green is mine (Bank change already decided by Mitchell in the 1:1). The 40k top-up on gr_qggxximtru stays with the other checkpoints in the Town Hall in-tray.
