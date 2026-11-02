---
id: "dc_rlhn5rbixa"
type: "report"
state: "building"
title: "gr_5ltmbf3a2f funded: plan cut into three steps (one per key result); steps 1 and 2 queued in parallel on the building, step 3 follows when the first building lands"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_ptei1pdy99","dc_pl034gahw2","dc_roeig7abhg"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Steps 1 (as_2m5yxrja95, Pix 3) and 2 (as_q5vonvpjqm, Pix 4) are running in lane grant gr_5ltmbf3a2f; step 3 gets queued when step 2's report lands. Plan on dc_pl034gahw2."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-01T02:06:21.768Z"
sessionId: "se_o5ic0e2z3z"
assignmentId: "as_pdibd230de"
costUsd: 1.96415555
tokens: 98208
turns: 15
createdAt: "2026-11-01T02:06:00.464Z"
updatedAt: "2026-11-01T02:06:21.768Z"
---
## What I did
Read the grant's findings ([dc_ptei1pdy99](../../note/2026-11/2026-11-01-findings-a-hosted-collective-stalls-at-birth-holly-ei1pdy99.md)), the hosted-collectives topic page ([dc_pl034gahw2](../../wiki/2026-11/2026-11-01-hosted-collectives-first-run-034gahw2.md)), the root-captain page ([dc_roeig7abhg](../../wiki/2026-11/2026-11-01-root-goal-always-has-a-captain-mt-cyd2t5ioob-d7-eig7abhg.md)) and the code behind them (migration 061, hub.ts, seed.ts, docs/hosted-collectives.md step 5, main.ts hosted runtime). Cut the plan into three steps, one per key result, and queued the first two on the building queue in lane grant (gr_5ltmbf3a2f). Rewrote [dc_pl034gahw2](../../wiki/2026-11/2026-11-01-hosted-collectives-first-run-034gahw2.md) with the plan. Mara's tell (no overlap with the post-mortem items) needs no reply.

## Findings
- **Step 1, as_2m5yxrja95** (queued; kr_n2zh7s6s2s, due 11-04): a hosted World never carries the Fund/Join/Trust pillars (migration 061 inserts them everywhere); an idempotent ensure step retires them when empty, so Hollyville's three go on the next boot; review-deck.ts must not assume them; a test proves root = the Start goal, founder = captain (already seeded by D7, af85f2a; verified, not rebuilt) and the Workshop's pillars untouched. Live check as a guest: GET /hollyville/api/goals shows root "Make money", owner Edward Li, no children.
- **Step 2, as_q5vonvpjqm** (queued, in parallel; kr_god7otzibq, due 11-05): Start creates one goal-directed building under the root with a manager-resident at an in-process desk (hosted limits of step 5), also on open for an existing hosted collective with none, so Hollyville serves as the live check at /hollyville/api/town; a keyless founder's HUD shows "Add your API key to start" linking to the Bank. The full HUD check needs a hosted admin's sign-in: the fork reports what Mitchell would click.
- **Step 3** (not yet queued; kr_f722z9ut50, due 11-06): with a key, the hosted runtime's explore tick reserves a chunk and the resident files a grant proposal to the founder's in-tray, billed on the founder's key input; fix what breaks. It needs step 2's building, so I queue it when step 2's report lands. Its live check needs a throwaway collective started from the homepage with a key (Mitchell or a test account): that goes in the rollup's "Your call" when step 3 is ready.
- Both step forks touch hub.ts open()/create and seed.ts; each was told to merge main before merging. Migration numbers: 078 highest on main, 077 taken by open PR #238.
- Budget: 500,000 tokens granted; steps told to stay near 150,000 / 200,000; step 3 gets the rest, under the 400,000 stop condition.

## What I need from you
Nothing needed.
