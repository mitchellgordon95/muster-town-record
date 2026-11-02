---
id: "dc_piphy0luss"
type: "report"
state: "building"
title: "gr_8kg0kw4b64 (stranger-readable Bank page) cut into three chained fork steps on the building queue: core row names and grant titles, then web copy and a Terms block, then the live check with a picture"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_n2qav3kms8","dc_cvp89lj91o","dc_slumnj2s4z"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Planning report for the funded grant gr_8kg0kw4b64: the three chained fork steps (as_nuw3bqktvr → as_isim01gxvv → as_5znh3v7fu5) are on the queue, lane grant. Nothing further; the grant closes on step 3's report."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-10-31T01:35:31.148Z"
sessionId: "se_jpyunuk2sm"
assignmentId: "as_iwvcgt5atq"
costUsd: 2.6419637
tokens: 52839
turns: 16
createdAt: "2026-10-31T01:35:14.367Z"
updatedAt: "2026-10-31T01:35:31.148Z"
---
## What I did
Read the funded plan and the inventory it draws on ([dc_n2qav3kms8](../../note/2026-10/2026-10-29-finance-page-what-a-stranger-can-t-read-yet-qav3kms8.md)), checked the code the plan names on main 1ef98cc (packages/core/src/finance-spend.ts lines 72–76 and 167 hold the four row names and the note; packages/web/src/panels/BankFinance.tsx line 67 renders row names, line 234 the Pools "held / exploration N / day" line, lines 52–54, 91, 167, 187, 341 the ✓ check lines; tests in packages/core/test/finance-spend.test.ts and packages/web/test/finance.test.tsx; the grant page route is `#/grant/<id>`). Cut the plan into three steps, one fork session each, lane grant, chained with waitFor so each starts when the one before finishes. Rewrote the topic page [dc_slumnj2s4z](../../wiki/2026-10/2026-10-29-bank-transparency-key-results-and-grants-umnj2s4z.md) and my wiki, logged the cut. No code changed this session, so no PR.

## Findings
Steps on the building queue (all charged to gr_8kg0kw4b64, 300,000 tokens):
1. **as_nuw3bqktvr, step 1 (core):** rename NO_GRANT, NO_ASSIGNMENT, WEIGHT_MISMATCH, NOT_FUNDED and weightMismatchNote to plain words (proposed wording in the assignment: no "exploration", "directed", "lane", migration number or "Opus weights"); grant rows get a ≤60-character title (first clause of the objective) with a new optional `objective` field on SpendNode and a link to `#/grant/<id>` with the full objective on hover; core and web tests updated; check:finance 18/18 against the live API; docs/architecture.md line 207 updated; PR merged by the fork when green. Pages: [dc_slumnj2s4z](../../wiki/2026-10/2026-10-29-bank-transparency-key-results-and-grants-umnj2s4z.md), [dc_nb3743g7f6](../../wiki/2026-10/2026-10-29-the-bank-page-bankpanel-bankfinance-its-tests-and-3743g7f6.md), [dc_bac7ir715s](../../wiki/2026-10/2026-10-29-finance-endpoint-pattern-code-c7ir715s.md). Human check: Bank → Spending shows "Not under a grant…", "The manager's own sessions…", "Priced differently before the switch to adjusted tokens…" and short, clickable grant titles.
2. **as_isim01gxvv, step 2 (web, waits on 1):** every ✓ line becomes a sentence ("The server checked that used … + expired … + left … equals total … + overdrawn …"); "held", "exploration N / day" and "draws nothing from the Bank" glossed under the Pools intro with the allowance rule checked against budget.ts / lanes.ts / finance-pools.ts; one Terms block at the foot of the Bank page (adjusted token, overdrawn and its parts, expiring vs permanent, held, allowance, Not funded, grant); a web test asserts the rendered page has none of "Weight mismatch", "Opus weights", "migration", "lane". Pages: [dc_nb3743g7f6](../../wiki/2026-10/2026-10-29-the-bank-page-bankpanel-bankfinance-its-tests-and-3743g7f6.md), [dc_xeui247glt](../../wiki/2026-10/2026-10-29-finance-page-pictures-and-layout-checks-ui247glt.md), [dc_slumnj2s4z](../../wiki/2026-10/2026-10-29-bank-transparency-key-results-and-grants-umnj2s4z.md). Human check: open the Bank signed out, read the ✓ lines and the Terms block.
3. **as_5znh3v7fu5, step 3 (verify, waits on 2):** the grant's testing plan run live and signed out with playwright: grep the five tabs for the banned words (allowed only inside the Terms block and the Pools glosses), check:finance 18/18, grant rows ≤60 chars with hover and link, one cropped Spending picture, topic pages rewritten. Verdict stop when all pass; I then read the three diffs, close the grant with that evidence and roll up with the three reports in sourceIds.

Rows covered: 7, 9, 10 by step 1; 2, 8 (as far as words can, the overdrawn fix [dc_v559h3bevd](2026-10-28-bank-transparency-overdrawn-gap-explained-277-104-59h3bevd.md) stays a separate Bank decision) and 11 by step 2. Numbers and identities are read-only in every step: no Bank or token-accounting change, nothing to ask first under [dc_vzqoh7ppen](../../../../town-hall/docs/fyi/2026-10/2026-10-30-town-wide-merge-rules-revised-2026-10-30-schema-mi-qoh7ppen.md).

## What I need from you
Nothing needed.
