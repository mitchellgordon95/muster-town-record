---
id: "dc_qhyvyyxez6"
type: "report"
state: "building"
title: "Secretary step 3e: digest reads asks through rollupAsks, Needs lines can be overtaken; PR #345 parked on CI"
authorId: "ag_3vxowx0juw"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. PR #345 (digest reads asks through rollupAsks, Needs lines overtaken) is parked on CI; as_iindwss0nc continues it (merge if green, no redeploy, park on the merge sha). Folds into rollup 47 with the live checks of #346/#347."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-04T20:01:40.386Z"
sessionId: "se_rao193btl7"
assignmentId: "as_tim030xku8"
costUsd: 0.8394816000000002
tokens: 41974
turns: 20
createdAt: "2026-11-04T20:01:30.785Z"
updatedAt: "2026-11-04T20:01:40.386Z"
---
## What I did
I switched the Secretary's `rollupCalls()` (packages/core/src/secretary.ts) to Teo's `rollupAsks(parseRollup(body))`, so the digest reads a rollup's asks from the same place as the deck and the in-tray. I also made a rollup's Needs lines count as asks that can be overtaken, added a core test, and opened draft PR https://github.com/mitchellgordon95/muster-town/pull/345. It is parked on CI.

## Findings
- Teo's `rollupAsks` already includes the "## Needs from Mitchell" lines, minus the generated "Already waiting" line and "Nothing needed". So the only new logic is a private `needsOvertaken()`:
  - A Needs line naming a grant that was decided after the rollup goes to **Already overtaken**. Decided means fund, reject, continue, adjust, cut, close, stop or withdraw in the grant's history.
  - So does a Needs line naming a retainer (sc_…) that is now funded, rejected or ended.
  - A Needs line in words goes to **Questions in words** as `<Building> asks (dc_…): <line>`.
- Shipped items keep their existing `overtakenReason`. The old filter (`isNoCall`) is gone from secretary.ts. The dead-code check passes.
- Behaviour change: a rollup whose only live ask is a Needs line now counts as still asking. Filing the digest card no longer auto-archives it.
- New test: one rollup whose only Needs line asks to fund a grant that was funded afterwards lands in Already overtaken (`gr_… was funded after this ask`). Another rollup's Needs line in words lands in Questions in words. The test also checks `stillAsks` for both.
- Local results: core 756 tests and server 286 tests pass, and the deadcode and typecheck steps pass. One full `npm run check` on the desk failed at the tests step after 10 min, and its output didn't say which workspace. The `--fast` run of the affected tests (738 and 220) passed. CI on PR #345 will settle it.
- Topic page [dc_t20pm17xh1](../../wiki/2026-11/2026-11-04-the-secretary-gr-kdlogzzo5s-0pm17xh1.md) is rewritten with the plan.
- On resume: if green, mark ready and merge. Don't redeploy ([dc_uzwcg5xw3u](../../../../town-hall/docs/fyi/2026-11/2026-11-04-do-not-call-redeploy-after-a-merge-ci-deploys-gree-wcg5xw3u.md)). Then park on `{deploy: <merge sha>}` and read GET /api/intray/digest.

## What I need from you
Nothing needed.
