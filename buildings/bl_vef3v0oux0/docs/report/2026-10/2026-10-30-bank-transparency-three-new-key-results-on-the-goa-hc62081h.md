---
id: "dc_tlhc62081h"
type: "report"
state: "building"
title: "Bank Transparency: three new key results on the goal (adjusted-token mix, a stranger can read the Bank page, no unpaid usage) for you to keep or cut; one grant proposed; building no longer blocked"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_cvp89lj91o","dc_gl478hfx6d"],"urls":["https://muster.town/api/finance/spend","https://muster.town/api/finance"]}
tags: ["rollup"]
verdict: "stop"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"1:1: Mitchell and Pix\": Bank Transparency (Nell) audits and enforces one credential per session after the 2026-10-30 post-mortem (dc_bq7yfn5dr8). Mitchell's worry: Budget.fundingFor or"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-30T23:36:51.575Z"
sessionId: "se_xs866s9cxm"
assignmentId: "as_h7tbot1pca"
costUsd: 2.95665565
tokens: 59133
turns: 24
createdAt: "2026-10-30T21:06:15.162Z"
updatedAt: "2026-10-30T23:36:51.575Z"
---
Live commit def72e8 (21:03Z). The building was blocked (all four original key results met and archived, none open). I wrote three new ones from your 1:1 ask and the building's findings; this rollup is where you keep, cut or reword them.

## Shipped

**1. Three key results written on the Bank Transparency goal**
**What it is:** The goal "Users can review a collective's finances at a glance" now has three open key results, each with a how-to-check line (kr_fydnpd8ok2, kr_zjawesqcyp, kr_jksobb0bwo; sources [dc_i2ln43k253](../../meeting-notes/2026-10/2026-10-30-1-1-mitchell-and-nell-notes-ln43k253.md), [dc_n2qav3kms8](../../note/2026-10/2026-10-29-finance-page-what-a-stranger-can-t-read-yet-qav3kms8.md), [dc_cvp89lj91o](2026-10-28-not-funded-row-split-live-in-code-weightmismatch-c-p89lj91o.md)).
- Adjusted-token mix (your ask in our 1:1 [dc_i2ln43k253](../../meeting-notes/2026-10/2026-10-30-1-1-mitchell-and-nell-notes-ln43k253.md)): the Bank's Tokens tab states what an adjusted token is as one global mix (x% input, y% cache read, z% cache write, w% output), recomputed daily from the usage logs, and every adjusted-token figure in the town is computed from that one record. The work is already scheduled as the directed job sc_p5oj6u7pks (fires 2026-11-01 02:00Z, after Core's refactor); no grant, since you said grants are changing.
- A stranger can read the Bank page: every term defined on the page or in one linked glossary, no internal names (migration numbers, model weights, lanes) in row names or notes. Rows 2 and 7–11 of Nell 1's inventory [dc_n2qav3kms8](../../note/2026-10/2026-10-29-finance-page-what-a-stranger-can-t-read-yet-qav3kms8.md) are what's left; the server-built Spending row names ("Weight mismatch… Opus weights", "No grant (exploration, directed…)") are the biggest items. Proposal gr_8kg0kw4b64 (300k) is in your in-tray for it.
- No work session goes unpaid: the Spending tab's "Not funded" row (195,957 adj. tokens, usage the Bank never debited) stops growing, and its note says the cause and whether it was charged back or written off. It has not grown between 2026-10-29 and 2026-10-30. Closing it means a Bank change (the recordUsage-only branch when a building's remaining is ≤ 0), so it has no proposal until you say charge back or write off.
**What you'd see:** Building → Bank Transparency → Settings (or the building board): the three key results, status not-started. No UI or API change in the town; nothing to picture.
**Your call:** Keep, cut or reword each of the three. If you cut the third, I drop the unpaid-usage question for good.

## Decided
- [dc_cvp89lj91o](2026-10-28-not-funded-row-split-live-in-code-weightmismatch-c-p89lj91o.md) (unpaid-usage split and SQL) → source for kr_jksobb0bwo; decided approve earlier.
- [dc_gl478hfx6d](2026-10-28-bank-transparency-spend-by-building-grant-assignme-478hfx6d.md) (spend by building/grant/assignment live, not-funded explained) → source for kr_jksobb0bwo; decided approve earlier.
- [dc_i2ln43k253](../../meeting-notes/2026-10/2026-10-30-1-1-mitchell-and-nell-notes-ln43k253.md) (1:1 notes, Mitchell and Nell) → no decision needed; the schedule sc_p5oj6u7pks it asked for is set, and its ask is now kr_fydnpd8ok2.
- [dc_n2qav3kms8](../../note/2026-10/2026-10-29-finance-page-what-a-stranger-can-t-read-yet-qav3kms8.md) (Nell 1's "what a stranger can't read yet", a note) → source for kr_zjawesqcyp and gr_8kg0kw4b64.
No resident reports landed since the last rollup ([dc_gmu7lw4u5h](2026-10-30-bank-transparency-the-finance-page-now-lives-on-th-u7lw4u5h.md), which you approved at 19:17Z).

## Key results
| Key result | Status | Grant | Spent / granted |
|---|---|---|---|
| kr_fydnpd8ok2 Adjusted-token mix, one global daily record | not-started | none (directed schedule sc_p5oj6u7pks) | 0 / 0 |
| kr_zjawesqcyp A stranger can read the Bank page | not-started | gr_8kg0kw4b64 proposed | 0 / 300,000 asked |
| kr_jksobb0bwo No work session goes unpaid | not-started | none (Bank change, your decision first) | 0 / 0 |

No funded grant. Today's spend by lane: exploration 0 / 0 tokens; directed 230,025 tokens at session start (this session, from the blocked-building assignment, adds to it).

## Needs from Mitchell
1. Approve these three key results for Bank Transparency's goal (keep, cut or reword each), or tell me what to change.

_Already waiting in your in-tray: 1 proposal (gr_8kg0kw4b64), 0 requests, 0 rollups._

## Key results I wrote (keep or cut: Building → Settings → Key results)
- created kr_fydnpd8ok2: "The Bank's Tokens tab states what an adjusted token is: one global mix (x% input, y% cache read, z% cache write, w% output) recomputed daily from the usage logs, and every adjusted-token figure in the town is computed from that one record." (how to check: Bank → Tokens & sources: one line with the four percentages and an "updated <date>" note; GET /api/finance returns the same mix with a computedAt under 24 h old; no hardcoded token weights remain in core/runtime (every caller reads the stored mix).; from [dc_i2ln43k253](../../meeting-notes/2026-10/2026-10-30-1-1-mitchell-and-nell-notes-ln43k253.md))
- created kr_zjawesqcyp: "A stranger can read the Bank page: every term on it is defined on the page or in one linked glossary, with no internal names (migration numbers, model weights, lanes) left in row names or notes." (how to check: Open https://muster.town/workshop/#/bank signed out: rows 2 and 7–11 of [dc_n2qav3kms8](../../note/2026-10/2026-10-29-finance-page-what-a-stranger-can-t-read-yet-qav3kms8.md) are fixed (✓ lines read as sentences; no "Weight mismatch", "Opus weights", "exploration", "held" without a gloss; grant rows carry short titles); npm run check:finance still passes.; from [dc_n2qav3kms8](../../note/2026-10/2026-10-29-finance-page-what-a-stranger-can-t-read-yet-qav3kms8.md))
- created kr_jksobb0bwo: "No work session goes unpaid: the Spending tab's "Not funded" row (195,957 adj. tokens on 2026-10-30: usage the Bank never debited) stops growing, and its note says the cause and whether the amount was charged back or written off." (how to check: Bank → Spending: "Not funded" (GET /api/finance/spend notFunded) equals the previous day's value two days running after the fix; the read-only SQL in [dc_cvp89lj91o](2026-10-28-not-funded-row-split-live-in-code-weightmismatch-c-p89lj91o.md) returns no usage rows without a debit after the fix date; the row's note names the cause.; from [dc_cvp89lj91o](2026-10-28-not-funded-row-split-live-in-code-weightmismatch-c-p89lj91o.md), [dc_gl478hfx6d](2026-10-28-bank-transparency-spend-by-building-grant-assignme-478hfx6d.md))
