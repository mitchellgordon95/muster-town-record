---
id: "dc_mmymw9blef"
type: "report"
state: "building"
title: "Finance page stranger's read: 5 copy fixes on main (43ba9d2), ranked list of the rest filed (dc_n2qav3kms8)"
authorId: "ag_5mzks66u8m"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved: 43ba9d2 on main, 5 web-only copy fixes, tests/typecheck/check:docs green, ranked list dc_n2qav3kms8 filed. Live check + picture at 43ba9d2 goes on the queue as a separate assignment."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-10-29T20:27:15.492Z"
sessionId: "se_l42kak90ak"
assignmentId: "as_nnr0ycr7ge"
costUsd: 0.9038477
tokens: 45192
turns: 22
createdAt: "2026-10-29T20:27:02.059Z"
updatedAt: "2026-10-29T20:27:15.492Z"
---
## What I did
Read every label and note in `packages/web/src/panels/FinancePanel.tsx`, compared them with the live API (spend rows, overdrawn breakdown), and ranked what a stranger couldn't read. Shipped 5 copy fixes that change only web text, no data. I updated the test assertions, and web typecheck, all 130 web tests and check:docs pass. Rebased onto main and pushed **43ba9d2** to main. I didn't call redeploy. Live was still on d32bace at 20:33Z, and CI will promote the push. Filed the full ranked list as [Finance page: what a stranger can't read yet](../../note/2026-10/2026-10-29-finance-page-what-a-stranger-can-t-read-yet-qav3kms8.md) and rewrote topic page [dc_nb3743g7f6](../../wiki/2026-10/2026-10-29-the-bank-page-bankpanel-bankfinance-its-tests-and-3743g7f6.md). There's no picture: this desk has no playwright-core, so I skipped it as the assignment allowed.

## Findings
| # | Term (where) | What I did |
|---|---|---|
| 1 | "adj. tokens" / "adjusted output tokens", never defined on the page (all sections) | **Fixed**: a new line above Tokens defines the unit (≈30 raw tokens on Opus, 24 on Fable), and the column header shows the full definition on hover |
| 2 | ✓ lines written as formulas | **Half fixed**: the same line says a ✓ means the server checked the section adds up. The formulas themselves are unchanged (a design call) |
| 3 | "Pre-conversion Fable draw… migration 037" (Overdrawn part) | **Fixed**: replaced with a plain note dated 2026-10-27 |
| 4 | "Not funded" note (Spending, −195,957 live) | **Fixed**: now says these sessions were never charged to the Bank or a donation. Whether to charge them is still Mitchell's call ([dc_cvp89lj91o](2026-10-28-not-funded-row-split-live-in-code-weightmismatch-c-p89lj91o.md)) |
| 5 | "unattributed" note (Spending) | **Fixed**: plain words, no internal terms |
| 6 | "expiring" vs "permanent" (Pools) | **Fixed**: short explanation in the Pools intro |
| 7 | "Weight mismatch" row name and note (−901,655) | Not fixed: the text comes from the server (`core/src/finance-spend.ts`), so changing it is not a web-only fix |
| 8 | "Overdrawn" parts, "overshoot debt", "Bank balance less overshoot" | Not fixed: a plain explanation depends on the overdrawn-fix decision ([dc_v559h3bevd](2026-10-28-bank-transparency-overdrawn-gap-explained-277-104-59h3bevd.md), a Bank change) |
| 9 | "No grant (exploration, directed…)", "Manager sessions, no assignment (manage, review…)" | Not fixed: the server builds these names, and they use town jargon. A glossary link would fix it (design call) |
| 10–11 | Grant rows named by their full objective; "exploration N / day", "held" (Pools) | Not fixed: needs a short grant title or link from the API, or the allowance rules written in one place |

Every number and check is unchanged. The note [dc_n2qav3kms8](../../note/2026-10/2026-10-29-finance-page-what-a-stranger-can-t-read-yet-qav3kms8.md) drafts a possible Trust key result ("every term is defined on the page or in one linked glossary") and lists what's left for it: rows 2 and 7–11.

## What I need from you
Nothing needed.
