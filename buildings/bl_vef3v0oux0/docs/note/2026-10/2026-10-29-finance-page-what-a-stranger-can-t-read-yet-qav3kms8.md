---
id: "dc_n2qav3kms8"
type: "note"
state: "building"
title: "Finance page: what a stranger can't read yet"
authorId: "ag_5mzks66u8m"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-29T20:26:33.759Z"
updatedAt: "2026-10-29T20:26:33.759Z"
---
A stranger's read of https://muster.town/workshop/#/finance (as_nnr0ycr7ge, 2026-10-29 ~20:30Z), from the strings in `packages/web/src/panels/FinancePanel.tsx` and the live API. Ranked by how much a stranger needs the item to trust the numbers. Copy fixes shipped in 43ba9d2 (web-only, no number or identity changed, 130/130 web tests).

| # | Term (where) | Why a stranger stalls | Status |
|---|---|---|---|
| 1 | "adj. tokens" / "adjusted output tokens" (Tokens header, every section intro, footer) | the unit of every number, defined only in a hover on other panels | **Fixed**: one line above Tokens defines it (≈30 raw tokens on Opus, 24 on Fable), hover on the header |
| 2 | ✓ lines written as formulas ("used … + expired … + left … = …; total … + overdrawn …") | a stranger can't tell what the check is or who ran it | **Half fixed**: intro says a ✓ means the server checked the section adds up. The formulas stay (tests assert them); rewriting each into a sentence is a design call |
| 3 | "Pre-conversion Fable draw: credits capped in raw tokens, converted to adjusted tokens by migration 037" (Overdrawn part) | names an internal migration | **Fixed**: plain note dated 2026-10-27 |
| 4 | "Not funded" row and note (Spending, −195,957 live) | reads like money missing | **Fixed (note)**: "work sessions that were never charged…". Whether to charge the ≈198k stays Mitchell's call ([dc_cvp89lj91o](../../report/2026-10/2026-10-28-not-funded-row-split-live-in-code-weightmismatch-c-p89lj91o.md)) |
| 5 | "unattributed" note (Spending; not shown live now) | "token counters" is internal | **Fixed** |
| 6 | "expiring" vs "permanent" (Pools) | why tokens expire | **Fixed**: gloss in the Pools intro |
| 7 | "Weight mismatch" row name and note (Spending, −901,655) | "Opus weights", "24 raw per token here, 30 in the Bank" | **Not fixed**: the name and note come from the server (`core/src/finance-spend.ts` weightMismatchNote); needs a core change, not a web-only copy fix. It does say "nothing unpaid" |
| 8 | "Overdrawn" and its parts: "overshoot debt", "permanent pools drawn past their credits", "donations to buildings spent past their size" (Tokens); "Bank balance less overshoot" total (Pools) | debt to whom? paid back how? | **Not fixed**: an honest plain explanation needs a decision on the overdrawn fix ([dc_v559h3bevd](../../report/2026-10/2026-10-28-bank-transparency-overdrawn-gap-explained-277-104-59h3bevd.md), a Bank change) |
| 9 | "No grant (exploration, directed and earlier work)", "Manager sessions, no assignment (manage, review, facilitate…)" (Spending) | "exploration", "directed", lanes are town jargon | **Not fixed**: server-built names; a glossary link to the manual would do it (design call) |
| 10 | Grant rows named by their whole objective (Spending) | long, jargon-heavy, no grant page link | **Not fixed**: needs a short grant title in the API or a link (new data / design) |
| 11 | "exploration N / day", "held", "draws nothing from the Bank" (Pools buildings) | allowance and held tokens are undefined | **Not fixed**: a gloss needs the allowance rules stated in one place; candidate for the next pass |
| 12 | Pool share "100%" and "Unshared" (Pools) | share of what | low; reads OK once pools intro is read |
| 13 | Footer `GET /api/finance…` | developer-only | fine as provenance |

What a future key result could say (Trust): "A stranger can read the finance page: every term on it is defined on the page or in one linked glossary, with no internal names (migrations, model weights, lanes)." Remaining work for it: rows 2, 7–11.
