---
id: "dc_7pwe0il0vz"
type: "report"
state: "building"
title: "Bank Transparency: Fly hosting spend in dollars is live on the finance page (b380807), verified by a fork; nothing needed"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_h2ci5oic0o","dc_4brp83xn58"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-30T01:18:19.779Z"
sessionId: "se_x83jdt7pcq"
createdAt: "2026-10-30T00:01:54.024Z"
updatedAt: "2026-10-30T01:18:19.779Z"
---
Live commit at the fork's check: b380807 (health, 2026-10-29 23:56Z); 5b95c21 pushed since, redeploy queued.

## Shipped
**1. Hosting (Fly.io) spend in US dollars next to the token spend**
**What it is:** Your ask via Cleo (1:1 mt_s6f8mvjw9h): a new read-only endpoint GET /api/finance/fly estimates what the town costs on Fly from desk sessions' wall time times the desk Machine's $/h, per UTC day and per building, plus the town Machine's share, and the finance page shows it in a "Hosting (Fly.io)" section with a Today / 7-day / 30-day table, the Machine sizes and rates, a "Not counted" list, "How this is estimated" and a ✓ Adds-up line. Built in as_z99cbqvxtj ([dc_h2ci5oic0o](2026-10-29-fly-spend-next-to-token-spend-get-api-finance-fly-ci5oic0o.md), b380807), verified live by fork as_6ailpm6r90 ([dc_4brp83xn58](2026-10-30-fly-spend-verified-live-at-b380807-check-finance-1-rp83xn58.md): `npm run check:finance` 18/18 ✓, three new fly identity checks all diff 0). The fork found the per-building rows ran the amount into the session count and fixed the markup in 5b95c21 (web tests 141/141); a fork is queued to confirm that live once it deploys (as_5ruzjhg1vy).
**What you'd see:** Finance page, section "Hosting (Fly.io)", signed out: Today $1.09 (desks $0.65 + town $0.45), last 7 days $5.28, last 30 days $15.79 (desks $2.40 + town $13.39; 128.9 h of desk time over 902 sessions), "Daily desk cap: none set", both Machines shared-cpu-2x 2 GB at $0.0186/h, six building rows (Workshop 78.3 h $1.46 … UI/UX 1.1 h $0.02). Caveat shown on the page: the town Machine is counted for all 30 days though desk sessions only start on 10-20, so the town figure may be high; 862 of 902 sessions have no measured wall time and are timed from start/end stamps.
![Finance page Hosting (Fly.io): today, 7-day and 30-day dollars, desk cap row and the check line](/api/media/mf_cih2a45x9g.png)
**Your call:** None required. If you want hosting dollars tracked as a key result ("Anyone can see what hosting costs in dollars next to the tokens"), say so and I'll write it from the 1:1 notes and propose a grant; otherwise it stays a directed feature. The daily desk cap row fills in when Prod's desk-perf step 3 lands (Cleo, ms_dmzs997ow7).

## Decided
- [dc_h2ci5oic0o](2026-10-29-fly-spend-next-to-token-spend-get-api-finance-fly-ci5oic0o.md) → approve (my own directed work: /api/finance/fly + Hosting section on main at b380807; fork live check queued).
- [dc_4brp83xn58](2026-10-30-fly-spend-verified-live-at-b380807-check-finance-1-rp83xn58.md) → approve (fork Nell 1: verified live, 18/18 ✓, picture mf_cih2a45x9g, alignment fix 5b95c21; follow-up live check queued as as_5ruzjhg1vy, waits for the deploy).

## Key results
| Key result | Status | Spent / granted |
|---|---|---|
| kr_j9058i256a Funding sources with amount and date | met (grant closed) | — |
| kr_97kyvac8f4 Pools and per-building allocation | met (grant closed) | — |
| kr_mx4odqn5xt Used, remaining, projection | met (grant closed) | — |
| kr_q9oiu7a6ci Spending by building, grant, assignment | met (grant closed) | — |
No funded grant and no open proposal. Today's spend by lane: exploration 0 / 828,571 tokens; directed ≈185k tokens (as_z99cbqvxtj 162,953 + as_6ailpm6r90, source mt_s6f8mvjw9h).

## Needs from Mitchell
Nothing needed.

_Nothing else waiting in your in-tray._
