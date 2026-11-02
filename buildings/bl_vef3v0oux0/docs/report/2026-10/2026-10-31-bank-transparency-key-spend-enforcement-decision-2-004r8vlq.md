---
id: "dc_qf004r8vlq"
type: "report"
state: "building"
title: "Bank Transparency: key spend enforcement (decision 2) is shipped and live at b44a0b8: sessions are debited as they run, every token counts however a session ends, and Donate asks API-key donors to set a Console spend limit"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_36rwon5pq9","dc_2kao6k6npo","dc_ypviz48zl3","dc_lvdg60x2jx","dc_lz5g5rsv3c"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-31T01:31:00.649Z"
sessionId: "se_f5j1frx3ph"
createdAt: "2026-10-31T00:48:28.759Z"
updatedAt: "2026-10-31T01:31:00.649Z"
---
Live commit b44a0b8 (booted 2026-10-31 00:40Z); an image redeploy was called at about 00:52Z and restarts the server after this session, same commit. This rollup covers your decision 2 from the 1:1 with Pix (mt_x40qq8poc3); decision 1 was in the previous rollup ([dc_wc1aa3wi9i](2026-10-31-bank-transparency-one-credential-per-session-is-li-1aa3wi9i.md)).

## Shipped

**1. Sessions are debited as they run, and every token counts however a session ends ((b)+(c))**
**What it is:** The Bank now books a running debit for each session at most once a minute while it runs, and settles the exact total at the end, whether the session reports, crashes, is killed or just stops. Before, a session that ended without a report was never charged. The Town Hall (no Bank share) keeps the old usage-only path so its residents are not flipped out of budget. Invariant 13 in the finance checks covers it. PR #131, main b44a0b8; reports [dc_ypviz48zl3](2026-10-31-key-spend-enforcement-b-c-sessions-are-debited-as-viz48zl3.md) and [dc_lz5g5rsv3c](2026-10-31-b44a0b8-is-live-and-nothing-went-unpaid-notfunded-5g5rsv3c.md).
**What you'd see:** API only. Bank → Spending "Not funded" stayed at 195,957 adj. tokens from the 00:40Z boot through 00:46Z (it had been growing before). A host session that ended without a report (se_n00fno6nrq) added exactly 13,598 adj. tokens to both the usage ledger and the Bank's debit. `npm run check:finance` passes 18/18. One gap: the 3 desks kept busy at the 00:40Z image redeploy still ran the old desk image, so their sessions are charged in full at the end but not debited while running; the 00:52Z image redeploy recreates them, and a check at 01:10Z confirms a fresh desk session's counters rise.
**Your call:** Behaviour change in token accounting: a building whose budget runs out mid-session now overshoots past zero (the session finishes and the Bank shows the negative) instead of the usage landing in "Not funded". Say if you want sessions cut off at zero instead.

**2. Donate asks API-key donors to set a spend ceiling in the Anthropic Console ((a))**
**What it is:** One line under the API-key field in Bank → Donate, with a link to the Console workspace limits (limits are per workspace, not per key). A hint, not a gate. Commit 950ac73, verified live; reports [dc_2kao6k6npo](2026-10-31-key-spend-enforcement-a-spend-limit-line-under-a-p-ao6k6npo.md) and [dc_lvdg60x2jx](2026-10-31-key-spend-enforcement-a-is-live-the-spend-limit-li-dg60x2jx.md).
**What you'd see:** Bank → Donate, paste a key: the spend-limit line appears under the field.
![Donate: spend-limit line under the API key field](/api/media/mf_1jqfk6zphx)
**Your call:** None.

## Decided
- [dc_36rwon5pq9](2026-10-31-session-ended-without-a-report-key-spend-enforceme-rwon5pq9.md) → redirect (first (b)+(c) run died waiting on a background check; second attempt queued with foreground-only checks)
- [dc_2kao6k6npo](2026-10-31-key-spend-enforcement-a-spend-limit-line-under-a-p-ao6k6npo.md) → approve ((a) in Donate, main 950ac73)
- [dc_ypviz48zl3](2026-10-31-key-spend-enforcement-b-c-sessions-are-debited-as-viz48zl3.md) → approve ((b)+(c), PR #131, main b44a0b8)
- [dc_lvdg60x2jx](2026-10-31-key-spend-enforcement-a-is-live-the-spend-limit-li-dg60x2jx.md) → approve ((a) verified live, picture mf_1jqfk6zphx)
- [dc_lz5g5rsv3c](2026-10-31-b44a0b8-is-live-and-nothing-went-unpaid-notfunded-5g5rsv3c.md) → approve (b44a0b8 verified live on the host side; image redeploy called, desk check scheduled for 01:10Z)

## Key results
| Key result | Status | Grant | Spent / granted |
|---|---|---|---|
| kr_jksobb0bwo No work session goes unpaid ("Not funded" stops growing) | not-started (evidence accruing: 195,957 unchanged since the fix; daily 03:00Z checks on 11-01 and 11-02) | none funded (directed work) | – |
| kr_fydnpd8ok2 Adjusted-token mix stated on the Tokens tab | not-started (scheduled 2026-11-01 02:00Z, directed) | none funded | – |
| kr_zjawesqcyp A stranger can read the Bank page | not-started | proposal open | – |

Today's spend by lane: exploration 0 / 1,000,000 tokens; directed 451,154 tokens.

## Needs from Mitchell
1. A desk Machine kept busy during an image redeploy keeps its old image until the next image redeploy finds it idle, so new runtime code (like the running debit) is late on those desks. The durable fix is to recreate a stale Machine when a session starts. That is runtime code (redeploy.ts, desk fly.ts), not Bank code: say whether Bank Transparency should build it, or whether it stays with Workshop.

_Already waiting in your in-tray: 1 proposal (gr_8kg0kw4b64), 0 requests, 1 rollup ([dc_wc1aa3wi9i](2026-10-31-bank-transparency-one-credential-per-session-is-li-1aa3wi9i.md))._
