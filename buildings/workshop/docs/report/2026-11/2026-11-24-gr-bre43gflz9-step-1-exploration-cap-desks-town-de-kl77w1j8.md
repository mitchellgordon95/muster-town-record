---
id: "dc_jpkl77w1j8"
type: "report"
state: "building"
title: "gr_bre43gflz9 step 1: exploration cap = desks × town default, PR #598 merging on green"
authorId: "ag_bt89ijakjf"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-24T22:23:03.897Z"
sessionId: "se_l3n8b28eew"
assignmentId: "as_59xs8m0781"
costUsd: 3.8673401000000003
tokens: 193367
turns: 62
createdAt: "2026-11-24T22:23:03.858Z"
updatedAt: "2026-11-24T22:23:03.897Z"
---
## What I did
Built step 1 of gr_bre43gflz9 in PR #598 (https://github.com/mitchellgordon95/muster-town/pull/598, commit 1b5f5c97). Typecheck, check:docs and deadcode pass. The core, server and web suites pass: 329 files, 2038 tests. Parked to merge when green.

## Findings
- **The default and why:** the live /api/goals showed 22 desks under gl_town (town-hall 1, workshop 5, UI/UX 3, Bank Transparency 3, Prod 2, Code Legibility 3, Outreach 2, Onboarding 3) and a flat 500,000/day cap on the root. The seed `exploreTokensPerDeskPerDay` is **22,727**, so the root's derived cap on day one is **499,994/day**. The chunk seed `exploreChunkTokens` stays **100,000**.
- **The cap:** `exploreCapsOnPath(world, goalId)` gives every goal on the path a cap of `desksAt` × the default. `desksAt` is the desksTotalAt total when one is set, else desksUnder. `exploreCapAt`, `exploreBlock`, `goalFunding`, the lanes hold and the finance-limits cap all read it. The arguments changed from the goals repo to `world`; the return shape is unchanged.
- **Behaviour change I added:** a cap smaller than one chunk still lets one explorer a day start under that goal. A cap of 0 lets none. Without this rule, goals with 4 or fewer desks would never explore (4 × 22,727 = 90,908 is less than one 100k chunk). That covers Prod's 2-desk goal and the 3-desk building goals.
- **Onboarding's own 100,000 cap is now ignored.** Its goal gl_bl_hzjw0z0zlz gets 3 × 22,727 = 68,181, and under the rule above it still gets one explorer a day.
- **Settings:** both defaults are on `Town`, `TownDefaultsPatch`, `grantPricingOf` / `setGrantPricing` (logged as a system event), PUT /api/town/defaults and GET /api/town/pricing. They are also on a new Exploration section of the planning desk's Step sizes tab. The chunk now comes from the town default (`exploreRuleAt(world, …)`, so `chunkFrom` is always null). Explore on/off is still one rule inherited down the goal tree.
- **Old goal columns:** `exploreCapTokensPerDay` and `exploreChunkTokens` stay in the DB and PATCH still accepts them, but nothing reads them. The goal tree's `cap:<n>` ask button (ask-acts.ts) now writes a column nothing reads. Step 2 should remove it along with the editor fields.
- **Docs:** goals.md Finance section; how-work-gets-done.md §3 table and §8 (retitled "Exploration is capped by desks"); log entry in docs/log.d/2026-11-24-exploration-cap-from-desks.md. The topic page "Desks steer exploration (gr_bre43gflz9)" ([dc_aniy3498i7](../../wiki/2026-11/2026-11-24-desks-steer-exploration-gr-bre43gflz9-iy3498i7.md)) holds the plan for step 2.
- **Not yet checked live:** once the PR is live, GET /api/goals/gl_town funding.exploreCap should read 499,994 (22 × 22,727).

## What I need from you
Nothing needed.
