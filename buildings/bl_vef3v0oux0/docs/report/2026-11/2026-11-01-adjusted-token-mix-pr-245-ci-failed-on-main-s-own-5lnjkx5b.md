---
id: "dc_ye5lnjkx5b"
type: "report"
state: "building"
title: "Adjusted-token mix: PR #245 CI failed on main's own deadcode bug; merged fixed main (addfce2), check green, parked on CI"
authorId: "ag_d6sqg74d7x"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "PR #245 later merged as bf9bb3c, live at b2b8789."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-02T02:05:44.183Z"
sessionId: "se_x9z4f86jef"
assignmentId: "as_39n6qoitep"
costUsd: 0.6573464
tokens: 32867
turns: 10
createdAt: "2026-11-01T21:31:57.124Z"
updatedAt: "2026-11-02T02:05:44.183Z"
---
## What I did
CI failed on PR #245's head e2d33cf. The failure was at the deadcode step, on `YoureIn` in `web/hud.tsx`. That came from main, not from my PR: main fixed it in be51fee. I merged origin/main into the branch again and resolved two conflicts:
- **`docs/bank.md`:** kept the mix section and took main's new heading, "Unexpected out-of-tokens deaths (step 5)", because main removed the cap hold.
- **`core/bank.ts` imports:** took main's `caps` import and added back `splitByMix` and `TokenMix`.

The full `npm run check` passed locally in 7m13s (docs, deadcode, typecheck, all tests). I pushed the new head, **addfce2**. GitHub reports it MERGEABLE, and CI is running: https://github.com/mitchellgordon95/muster-town/pull/245

## Findings
- **Nothing is merged or redeployed yet.** That waits for CI to pass on addfce2.
- **PR #244 (usd) is still open.** Whichever of #244 and #245 merges second has to merge main first and keep both the mix and the usd block.
- **The plan is on the topic page [dc_ydgrv1arc3](../../wiki/2026-11/2026-11-01-adjusted-token-mix-what-1-adj-token-is-made-of-grv1arc3.md):**
  1. Once CI is green, check that the PR is still mergeable.
  2. Merge it and redeploy.
  3. Once it's live: run `check:finance`, read the live mix percentages, take a picture, and tell Teo.

## What I need from you
Nothing needed.
