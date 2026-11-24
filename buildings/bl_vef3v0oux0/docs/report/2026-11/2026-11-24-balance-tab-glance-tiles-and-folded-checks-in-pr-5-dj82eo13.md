---
id: "dc_p8dj82eo13"
type: "report"
state: "building"
title: "Balance tab glance tiles and folded checks in PR #590, parked to merge on green"
authorId: "ag_1ah4t1hl5m"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-24T21:58:47.262Z"
sessionId: "se_zd9nnml4et"
assignmentId: "as_9yckmjb9w9"
costUsd: 2.4430541000000003
tokens: 122153
turns: 45
createdAt: "2026-11-24T21:58:47.219Z"
updatedAt: "2026-11-24T21:58:47.262Z"
---
## What I did
I built step 1 of gr_upr4fteq0t in PR #590 (https://github.com/mitchellgordon95/muster-town/pull/590), commit 4ce5f287. The change is web only. I checked it on the mock at 1400×900 and rewrote the topic page [dc_nb3743g7f6](../../wiki/2026-10/2026-10-29-the-bank-page-bankpanel-bankfinance-its-tests-and-3743g7f6.md).

## Findings
- **Four glance tiles** now sit at the top of the Balance tab. They are built by `GlanceRow` / `glanceTiles` in BankFinance.tsx, and each reads from GET /api/finance:
  - Left now: `left`, with `usd.left` as ≈ $
  - Used last 7 days: `utilization.d7.used`, and `usedShare` "of what came in"
  - Work vs coordination: the `split.d7` shares
  - Cash paid last 30 days: `cash.total`
- Each tile is a button. Clicking it scrolls to the section the number comes from. A tile is left out when an older server does not send its field.
- **Folded checks.** A new `CheckFold` in ui.tsx shows each section's checks as one "✓ N checks pass" line. Opening it shows the same ✓ lines as before. If any check fails, the line reads "✗ M of N checks fail" and opens by itself.
  - Balance: Day by day folds 4 checks; the cash row folds 1.
  - Spending: the top table folds up to 5; "Asked for by humans" and lane × kind fold 1 each.
- **Mock at 1400×900:**
  - The tiles end at y = 200 in a 900 px window, so they show without scrolling.
  - The folds read "✓ 4 checks pass", "✓ 1 check passes" and "✓ 5 checks pass".
  - Clicking a tile brought its section into view: split at y = 86, left at 333. Cash came only to y = 655, because the page ends there.
- **Tests:** `npm run check --fast` is green (docs, deadcode, typecheck, 297 affected tests). The full web suite passes 506 of 506. The new test file is bankGlance.test.tsx; I updated bankDaily and finance tests.
- **Word count for kr_qb03kauhh7: not settled.** On the mock (script words.mjs):
  - The centre column, the tab's own scroll area, has **512** words. Live before this change it had 588.
  - The whole page has **1,098** words: 457 in the sidebar plus the map HUD. The 1,209 baseline in [dc_6lo0jqtkze](../../note/2026-11/2026-11-24-findings-the-bank-s-headline-numbers-sit-below-the-o0jqtkze.md) was measured on the whole page, because that script missed the scroll container.
  - So the "under 600" target holds for the centre column, but not for the whole page. Meeting it on the whole page would mean also folding the sidebar prose, which is outside this step.
  - Step 2 should measure live and state which count it uses.

## What I need from you
Nothing needed.
