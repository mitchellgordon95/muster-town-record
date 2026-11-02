---
id: "dc_s5f2j973pn"
type: "report"
state: "building"
title: "Overdrawn breakdown added to GET /api/finance and the finance page (draft PR #65, head b85dc96)"
authorId: "ag_t5p8jfp9fk"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved: overdrawn breakdown on GET /api/finance and the page (PR #65, b85dc96), read-only, no Bank rows touched. I'll merge it once CI (incl. typecheck) is green and queue the redeploy; your live check is queued to resume once b85dc96 is deployed."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-10-28T01:13:28.689Z"
sessionId: "se_wwabd4a97f"
assignmentId: "as_1oahguhoou"
costUsd: 0.7528467
tokens: 37642
turns: 22
createdAt: "2026-10-28T01:01:03.891Z"
updatedAt: "2026-10-28T01:13:28.689Z"
---
## What I did
- Added `overdrawnBreakdown` to `financeSummary` in `packages/core/src/finance.ts`, so it is served by GET /api/finance. It has four parts: `durableOvershoot`, `subscriptionOverdrawn`, `deletedCreditDebits` and `allocationOverspent`. `overdrawn` is now computed as their sum, so the parts always add up to it.
- Finance page (`FinancePanel.tsx`): under the Overdrawn row it lists the parts that aren't zero. The subscription part has the note "Pre-conversion Fable draw: credits capped in raw tokens, converted to adjusted tokens by migration 037."
- The change only reads existing ledgers. There is no schema change, no change to Bank accounting, and no Bank rows are touched.
- Also updated the web `Finance` type, the mock server and `docs/architecture.md`.
- Draft PR: https://github.com/mitchellgordon95/muster-town/pull/65. Head commit is **b85dc96**, on a branch merged with main at 84153bd.

## Findings
- **Tests:**
  - Core `finance.test.ts` passes 7/7. A new test checks that the four parts sum to `overdrawn` on mixed inputs: 250 + 70 + 40 + 35 = 395, and the sum check still passes. The real-Bank test now also checks that the parts sum to `overdrawn`.
  - Web `finance.test.tsx` passes 6/6. A new test checks that the listed parts sum to `overdrawn`, that zero parts are hidden, and that the migration 037 note is shown.
- **Typecheck: not completed.** `npm run typecheck` timed out on my desk after 500 s for core, web and server, so I couldn't confirm it here. CI (`ci.yml`) should check it on the PR before merging. The tests compile the changed files but don't type-check them.
- **Expected live once deployed:** durableOvershoot 256,870, subscriptionOverdrawn 277,104, deletedCreditDebits 0, allocationOverspent 66, summing to 534,040. These are the figures from [dc_4exx02zf9g](2026-10-28-the-277-170-overdrawn-gap-277-104-from-fable-sessi-xx02zf9g.md), which I haven't checked against live yet.

## What I need from you
Merge PR #65 once CI is green, including the typecheck, then redeploy. I'll check the live figures next session.
