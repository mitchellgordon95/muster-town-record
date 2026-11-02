---
id: "dc_4t7nyo7y02"
type: "report"
state: "building"
title: "PR #242 CI failed on knip (two unused exports); fixed as ee7c820, parked on CI again"
authorId: "ag_03fxbwsxj5"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Knip fix pushed; Pix 2's continuation on {pr: 242} merges, redeploys and live-checks. Tip kept: run `npm run check -- deadcode` before pushing."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-01T02:21:49.906Z"
sessionId: "se_f8tgncccp9"
assignmentId: "as_lmb4qf4bsh"
costUsd: 0.3622553
tokens: 18113
turns: 9
createdAt: "2026-11-01T02:18:44.639Z"
updatedAt: "2026-11-01T02:21:49.906Z"
---
## What I did
PR #242's CI failed at the deadcode step after 6 s. Knip flagged `FIRST_BUILDING_NAME` and `ensureFirstBuilding` in packages/server/src/hub.ts as unused exports. They are only used inside hub.ts, so I removed the `export` keyword from both. The branch was already up to date with main 08c16a7. I ran `npm run check -- --fast` (docs, typecheck, tests) and then `npm run check -- deadcode`; both passed. I pushed ee7c820 to the PR branch.

## Findings
- CI log run 41264376616: "Unused exports (2) FIRST_BUILDING_NAME hub.ts:39, ensureFirstBuilding hub.ts:48 … FAILED at deadcode". Local `--fast` skips deadcode, which is why Pix 4's local check showed green. Run `npm run check -- deadcode` before pushing.
- When CI is green: merge #242 (merge main first if it has moved), redeploy, park on the deploy. Then do the guest live check (/hollyville/api/town lists Workshop and a resident, /api/health commit, bundle string "Add your API key to start") and update [dc_7lpbltjy1j](../../wiki/2026-10/2026-10-31-rollup-37-materials-pbltjy1j.md) and [dc_pl034gahw2](../../wiki/2026-11/2026-11-01-hosted-collectives-first-run-034gahw2.md).
- Still needs a human, per [dc_y3fn93mu4l](2026-11-01-hosted-collectives-start-with-a-workshop-building-fn93mu4l.md): Mitchell signs in and presses **Start a collective** without a key. He should see the Workshop on the map and the HUD line "Add your API key to start".

## What I need from you
Nothing needed.
