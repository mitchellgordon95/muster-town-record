---
id: "dc_d7nlynpn3z"
type: "report"
state: "building"
title: "Bank Transparency: the Finance page is in draft PR #61 (it includes #60). Please merge #61 and redeploy."
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_4nz8b57os7"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"Town Hall town-hall\": Bank Transparency: Nell copies the Workshop board's merge rules (a manager merges their own building's green PR to main and redeploys without asking; ask Mitche"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T22:27:22.774Z"
sessionId: "se_6it3en7q1o"
createdAt: "2026-10-27T19:07:27.149Z"
updatedAt: "2026-10-27T22:27:22.774Z"
---
## Shipped
- Nothing is live yet.
- Step 2 of gr_gi5jbgzv4k is built: the public Finance page, at `#/finance` or the "$" button in the HUD. It is in draft PR #61 (commit b070f2f), which sits on top of #60 (GET /api/finance). The page shows:
  - total received
  - used, expired and left
  - overdrawn, in red
  - a sum check written out in numbers
  - a 30-day projection and how many days the tokens left will last
  - each pool, with the General pool shown as overdrawn by about 256,870
- All 80 web tests pass and typecheck is clean ([dc_4nz8b57os7](2026-10-27-finance-page-built-draft-pr-61-on-top-of-60-used-e-z8b57os7.md)).

## Decided
- [dc_4nz8b57os7](2026-10-27-finance-page-built-draft-pr-61-on-top-of-60-used-e-z8b57os7.md) (Asha, Finance page): approved. Step 3, verifying the page live and gathering evidence for the checkpoint, is queued for Asha (as_zi1s0q4xgq). It starts after the next redeploy.

## Key results
- kr_mx4odqn5xt (gr_gi5jbgzv4k): on track. 128,919 / 1,200,000 tokens spent. Steps 1 and 2 are built; step 3 waits on the merge and deploy.
- kr_j9058i256a, kr_97kyvac8f4, kr_q9oiu7a6ci: not started, no grant yet.
- Today's spend: exploration 39,966 / 828,571 tokens; directed 48,276 tokens.

## Needs from Mitchell
- Merge PR #61 (https://github.com/mitchellgordon95/muster-town/pull/61), then redeploy. #61 contains #60, so this replaces my earlier ask to merge #60 alone ([dc_gi9nmarefv](2026-10-27-bank-transparency-get-api-finance-is-ready-in-draf-9nmarefv.md)).
