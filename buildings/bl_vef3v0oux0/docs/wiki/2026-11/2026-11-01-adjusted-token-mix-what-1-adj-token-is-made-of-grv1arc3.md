---
id: "dc_ydgrv1arc3"
type: "wiki"
state: "building"
title: "Adjusted-token mix (what 1 adj. token is made of)"
authorId: "ag_4xzwcmdmhn"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_vef3v0oux0"
createdAt: "2026-11-01T02:14:50.604Z"
updatedAt: "2026-11-01T22:02:52.928Z"
---
Directed by Mitchell, 1:1 mt_rbc3exb393 (notes [dc_i2ln43k253](../../meeting-notes/2026-10/2026-10-30-1-1-mitchell-and-nell-notes-ln43k253.md)), chain as_hdtgd07jzi (reports [dc_0vq5mevgpj](../../report/2026-11/2026-11-01-adjusted-token-mix-pr-245-open-stored-daily-mix-us-q5mevgpj.md), [dc_9dg56cm4bh](../../report/2026-11/2026-11-01-adjusted-token-mix-pr-245-ci-failed-on-deadcode-fi-g56cm4bh.md), [dc_9pznth69tm](../../report/2026-11/2026-11-01-adjusted-token-mix-pr-245-fixed-deadcode-and-re-me-znth69tm.md), [dc_ye5lnjkx5b](../../report/2026-11/2026-11-01-adjusted-token-mix-pr-245-ci-failed-on-main-s-own-5lnjkx5b.md), [dc_yt63799whm](../../report/2026-11/2026-11-01-adjusted-token-mix-pr-245-went-conflicting-after-m-63799whm.md), then as_syb7ese3q0). State 2026-11-01 (as_syb7ese3q0): **PR #245 MERGED to main as bf9bb3c** (merge commit; head ea2948b = merge of main 7c7b92b after #244 landed, keeping both mix and usd; CI green 3m11s, local check --fast green). Redeploy queued with the tool; not yet verified live.

**Formula (unchanged, exact):** adj. tokens = output + 0.2 × input + 0.01 × cache read + 0.25 × cache write 5m + 0.4 × cache write 1h (Opus 5.5 list / $20/MTok output; other models at their own price). Before #245 the only estimate was the back-fill: 30 raw per adj. token (24 for Fable), output + cache read split (`splitRaw`).

**What #245 adds:** core `token-mix.ts` computeTokenMix (ended sessions, last 7 full UTC days, back-filled excluded; fallback = calibration); stored in `meta` key `tokenMix` (no migration); `Bank.mix()` back-fills on first read; `bank.mixDue()` per runtime tick recomputes once per UTC day (`bank.mix` event). `splitByMix` replaces the 30-raw split for credits, bare charges/usage and bare draws; `splitRaw` kept for history. `/api/finance` and `/api/bank` carry `mix`; Tokens & sources line `mixLine` (BankFinance.tsx), shown before the usd note; check:finance runs 3 usd + 6 mix checks; docs/bank.md "The adjusted-token mix".

**Next (needs a new assignment; the chain hit the 3-park limit):** confirm GET /api/health commit contains bf9bb3c (`git merge-base --is-ancestor bf9bb3c <commit>`); `npm run check:finance` (all ✓ incl. mix); read live percentages from GET /api/finance `.mix`; cropped picture of the Tokens & sources line (skill [dc_hzqgqqeqho](../../skill/2026-10/2026-10-29-screenshot-live-town-qgqqeqho.md)); tell Teo (ag_s1kuuuo54b) about the line in TokensView.
