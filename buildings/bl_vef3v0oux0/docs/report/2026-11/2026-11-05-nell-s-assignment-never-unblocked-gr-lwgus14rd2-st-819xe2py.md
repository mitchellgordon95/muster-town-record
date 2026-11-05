---
id: "dc_2t819xe2py"
type: "report"
state: "building"
title: "Nell's assignment never unblocked: gr_lwgus14rd2 step 3: manager wakes per building per day beside their cost, in the Spending drill-down and /api/finance/spend (kr_avafh64h02)"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: ["wait-expired"]
decision: "approve"
decisionNote: "The wait on step 2's chain expired because its tip (as_wd0gpawhhk, verify cache-miss alert live) is held at the grant's checkpoint. Step 3 doesn't depend on that verify (it builds on step 1's shape, live since b2282771), so I re-queue it without the wait as a plain grant-lane assignment; it stays held until Mitchell continues gr_lwgus14rd2."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-05T17:59:17.376Z"
assignmentId: "as_5xuggxsopv"
createdAt: "2026-11-05T17:58:52.048Z"
updatedAt: "2026-11-05T17:59:17.376Z"
---
Written by the town, not by Nell: this assignment was queued on 2026-11-04 17:58 UTC waiting on Nell 2's "gr_lwgus14rd2 step 2: daily cache-miss check and `alert: ca…" to finish, which didn't happen within 24 hours, so it was cancelled.

## Summary

Wait expired: gr_lwgus14rd2 step 3: manager wakes per building per day beside their cost, in the Spending drill-down and /api/finance/spend (kr_avafh64h02)

## The assignment

Key result kr_avafh64h02: the Bank shows manager wakes per building per day beside their cost (wakes, adj. tokens, cost per wake and per decided report), so four wakes in fifteen minutes for four reports is a visible number. Check: Bank → Spending, building drill-down: a 'Manager wakes' line per day (count, adj. tokens, per wake, per decision); the same in GET /api/finance/spend.

Plan page [dc_qnpvanlfsb](../../wiki/2026-11/2026-11-04-token-cost-legible-gr-lwgus14rd2-plan-and-state-pvanlfsb.md) has the file pointers. Steps 1 and 2 landed first (as_m28p9taow1, as_gc6u3sk0wf): build on step 1's window + per-building shape. Do, in one PR:
1. Core, pure: `managerWakes(sessions, docs, window)` → per building per UTC day: wakes = sessions with purpose `manage` of that building's manager; adj. tokens (and ≈ $) summed; decided reports = docs with decidedBy = the manager and decidedAt within one of those sessions' [startedAt, endedAt]; per wake = tokens / wakes; per decision = tokens / decided (null when 0 decided). Also a 7-day total line. Say in the shape comment what "decided" counts (reports and flags decided via review; rollups filed count as a separate number if cheap).
2. Server: on GET /api/finance/spend (same ?window= as step 1) a `managerWakes` block keyed by building id, days newest first; check:finance line (Σ wake tokens ≤ Σ manage-session tokens of the window; days sum to the total).
3. Web: Spending building drill-down (BankSpending.tsx level 2) gets a 'Manager wakes' line per day (count, adj. tokens, per wake, per decision) under the grants rows, folded when there are more than 7 days; level 1 shows the town-wide 7-day total in the sidebar. Mock rows so web tests cover it.
4. Unit tests for the join (a decision inside a session counts, outside does not; two wakes in one day sum). `npm run typecheck`, core + server + web tests, check:finance against the mock.
Then push, draft PR, park on {pr: N}; when green merge, redeploy, park on {deploy: sha}; verify live signed out at 1400×900: one cropped picture of the line in one building's drill-down ([dc_xeui247glt](../../wiki/2026-10/2026-10-29-finance-page-pictures-and-layout-checks-ui247glt.md) method), today's live numbers for Bank Transparency and Town Workshop, check:finance all ✓, rewrite [dc_qnpvanlfsb](../../wiki/2026-11/2026-11-04-token-cost-legible-gr-lwgus14rd2-plan-and-state-pvanlfsb.md) (state: the three KRs with evidence so the grant can be closed) and [dc_tkzoy81p4b](../../wiki/2026-10/2026-10-29-the-three-finance-endpoints-their-sum-checks-and-l-zoy81p4b.md). Bank code is ours: merge without asking.

## Proposal for next session

gr_lwgus14rd2 step 3: manager wakes per building per day beside their cost, in the Spending drill-down and /api/finance/spend (kr_avafh64h02)

Acknowledge to drop it, Continue to queue it again without the wait, or Redirect it with a note.
