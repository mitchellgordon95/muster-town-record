---
id: "dc_ufvodjfthj"
type: "report"
state: "building"
title: "Bank Transparency: forks running, four fork assignments landed (finance copy fixes, one-command live check, docs drift); all four KRs met, nothing needed"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_u3y1j8t520","dc_43ir7grxp2","dc_mmymw9blef","dc_fdadcf45d2","dc_blvwon09hv"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-29T21:00:00.844Z"
sessionId: "se_yw35nc4sig"
createdAt: "2026-10-29T20:33:30.961Z"
updatedAt: "2026-10-29T21:00:00.844Z"
---
Live at 3e32e08 (20:31Z). Budget mode flipped to forks at 15:46Z; four directed fork assignments ran from the building queue since, all four done and approved, queue empty.

## Shipped

**1. Finance page reads plainly for a stranger (43ba9d2)**
**What it is:** Five web-only copy fixes on the finance page: a unit line ("Every amount here is in adj. tokens…", what a ✓ line means) above the Tokens section, the overdrawn note no longer says "migration 037", plainer "Not funded" and "unattributed" notes, and a gloss on expiring vs permanent pools. No data or API change. Fork reports [dc_mmymw9blef](2026-10-29-finance-page-stranger-s-read-5-copy-fixes-on-main-ymw9blef.md) (the fixes), [dc_blvwon09hv](2026-10-29-finance-copy-fixes-43ba9d2-verified-live-tokens-pi-vwon09hv.md) (verified live); the ranked remainder that would need new data is [dc_n2qav3kms8](../../note/2026-10/2026-10-29-finance-page-what-a-stranger-can-t-read-yet-qav3kms8.md).
**What you'd see:** https://muster.town/workshop/?guest#/finance signed out: the unit line sits above the Tokens heading; total 68,263,410 adj. tokens, used 40,406,624, Bank balance 8,761,565 at 20:31Z.
![Finance page: unit line above the Tokens section (43ba9d2)](/api/media/mf_cyovw6sxcx.png)
**Your call:** None.

**2. One-command live finance check (3e32e08)**
**What it is:** `npm run check:finance [baseUrl]` (scripts/finance-check.ts) hits the four /api/finance* endpoints of any base URL and checks 15 identities within and across them (used + expired + left = total + overdrawn; spend.used = finance.used; sources sum to total received; pool draws and Bank balance match), exit 1 on any ✗. Fork report [dc_fdadcf45d2](2026-10-29-one-command-live-finance-check-on-main-3e32e08-npm-adcf45d2.md).
**What you'd see:** Tooling, no page change. Run against https://muster.town at 20:31Z: 15/15 ✓, all four diffs 0.
**Your call:** None.

**3. Finance docs caught up with the code (d9a656b)**
**What it is:** docs/architecture.md now documents all four finance endpoints (/api/finance, /spend, /sources, /pools), the weight-mismatch note on /spend, and the Finance panel description (Bank pools table is the fallback); check:docs green. Fork report [dc_43ir7grxp2](2026-10-29-finance-docs-drift-fixed-architecture-md-documents-ir7grxp2.md).
**What you'd see:** Docs only, no page change.
**Your call:** None.

## Decided
- [dc_u3y1j8t520](2026-10-29-forks-step-2-started-for-bank-transparency-mitchel-y1j8t520.md) → approve (my report: forks step 2 started, three directed assignments queued)
- [dc_43ir7grxp2](2026-10-29-finance-docs-drift-fixed-architecture-md-documents-ir7grxp2.md) → approve (Nell 1: docs drift d9a656b)
- [dc_mmymw9blef](2026-10-29-finance-page-stranger-s-read-5-copy-fixes-on-main-ymw9blef.md) → approve (Nell 1: 5 copy fixes 43ba9d2; queued the live-verify + picture follow-up)
- [dc_fdadcf45d2](2026-10-29-one-command-live-finance-check-on-main-3e32e08-npm-adcf45d2.md) → approve (Nell 1: check:finance 3e32e08)
- [dc_blvwon09hv](2026-10-29-finance-copy-fixes-43ba9d2-verified-live-tokens-pi-vwon09hv.md) → approve (Nell 1: 43ba9d2 verified live, picture, 15/15 ✓)

## Key results
No funded grant: all four grants are closed and all four key results are marked met (kr_j9058i256a, kr_97kyvac8f4, kr_mx4odqn5xt, kr_q9oiu7a6ci).

| Key result | Status | Spent / granted |
|---|---|---|
| kr_97kyvac8f4 pools and per-building allocation (gr_mijwhoiy2f, closed) | met | 200,677 / 300,000 |
| kr_j9058i256a funding sources (gr_gbpbbwy9b8, closed) | met | closed earlier |
| kr_mx4odqn5xt used / remaining / projection (gr_gi5jbgzv4k, closed) | met | closed earlier |
| kr_q9oiu7a6ci spend by building, grant, assignment (gr_8gtgmd828o, closed) | met | closed earlier |

Today's spend by lane: exploration 84,535 / 828,571 tokens; directed 317,157 tokens (the four fork assignments trace to your forks flip, [dc_obd6i8koz3](../../../../../library/human-report/2026-10/2026-10-29-re-bank-transparency-forks-step-1-done-flip-budget-d6i8koz3.md)). The building goal has no open key result; the next work needs a new KR from a 1:1 (a candidate Trust KR, "a stranger can read the finance page: every term defined on the page or in one linked glossary", is drafted in [dc_n2qav3kms8](../../note/2026-10/2026-10-29-finance-page-what-a-stranger-can-t-read-yet-qav3kms8.md)) or exploration against a stated gap.

## Needs from Mitchell
Nothing needed.

_Nothing else waiting in your in-tray._
