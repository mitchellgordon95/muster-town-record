---
id: "dc_9dg56cm4bh"
type: "report"
state: "building"
title: "Adjusted-token mix: PR #245 CI failed on deadcode, fixed (dd6d3b8) and marked ready; parked on CI again"
authorId: "ag_d3781203um"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Acknowledged: deadcode fix dd6d3b8, #245 ready. The parked continuation as_ffomw2mhul ({pr:245}) carries on: merge main first if #244 lands and leaves #245 CONFLICTING, then merge, redeploy, live check, picture, tell Teo."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-01T02:23:10.492Z"
sessionId: "se_i9c8ulqnjs"
assignmentId: "as_4mjkdvsgb1"
costUsd: 0.375836
tokens: 18792
turns: 10
createdAt: "2026-11-01T02:22:51.942Z"
updatedAt: "2026-11-01T02:23:10.492Z"
---
## What I did
CI on PR #245 failed. The cause was the deadcode check: `MIX_WINDOW_DAYS` was exported from `packages/core/src/token-mix.ts` but never used outside that file. I made it module-private and merged main (08c16a7) into the branch. The full `npm run check` then passed locally: docs, deadcode, typecheck and all tests. I pushed the fix as dd6d3b8 and marked #245 ready for review: https://github.com/mitchellgordon95/muster-town/pull/245

## Findings
- No change to the feature itself. The formula is the same as in [dc_0vq5mevgpj](2026-11-01-adjusted-token-mix-pr-245-open-stored-daily-mix-us-q5mevgpj.md): adj. tokens = output + 0.2 × input + 0.01 × cache read + 0.25 × cache write (5 min) + 0.4 × cache write (1 h).
- #245 is not merged and not live yet. The live percentages, the picture and the message to Teo all wait until it is merged and deployed.
- docs/manual.md is at 1,891 of its 1,900-word cap.
- The plan for the next session is on topic page [dc_ydgrv1arc3](../../wiki/2026-11/2026-11-01-adjusted-token-mix-what-1-adj-token-is-made-of-grv1arc3.md):
  1. When CI is green, merge and redeploy.
  2. Once it is live, run `check:finance`, read `.mix` from `/api/finance`, take a cropped picture of the Tokens & sources line, and tell Teo.

## What I need from you
Nothing needed.
