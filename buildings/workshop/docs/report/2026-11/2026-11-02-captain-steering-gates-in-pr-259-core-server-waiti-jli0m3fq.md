---
id: "dc_z4jli0m3fq"
type: "report"
state: "building"
title: "Captain steering gates in PR #259 (core+server), waiting on CI"
authorId: "ag_i4ogy4bus9"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Step 1 of gr_zsm1piyqyx built in PR #259 (1c8f714); the continuation as_l3oe8cqb93 (merge if green, redeploy, rollup 38 line) resumes on CI. The 1:1 \"member outside, staff inside\" reading is what goes in the rollup's Your call for kr_k2gesp1b5e."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-02T03:12:41.502Z"
sessionId: "se_l6s1ne5mul"
assignmentId: "as_5hn5a01ot1"
costUsd: 1.4715721000000002
tokens: 73579
turns: 39
createdAt: "2026-11-02T03:12:16.929Z"
updatedAt: "2026-11-02T03:12:41.502Z"
---
## What I did
Built gr_zsm1piyqyx step 1 (core + server, no web/Bank change) and opened draft PR https://github.com/mitchellgordon95/muster-town/pull/259 (head 1c8f714). Parked on its CI.

## Findings
- New `Goals.captainsBuilding(actor, buildingId)` (core goals.ts): true only for a human who captains the building's goal or one above it. False for agents, the system, the Town Hall and unknown buildings.
- It sits beside the existing role checks (never in place of them) in: in-tray report `canDecide` (intray-routes.ts), the `review` verb, `archiveReport`, meeting speak/end (ops.ts), `createMeeting` and `isOneOnOneStaff` (meetings.ts; a captain's 1:1 has no member block, so it counts as a human source), and `plantFlag` (domain.ts). lanes.ts `humanSource` needed no change.
- 1:1 vs. the KR wording: outside their subtree a captain's default 1:1 **still opens**, as a plain member's (Mitchell's gr_58n37j410s member rule is kept). An agent-targeted 1:1, flags and rollup decisions return 403 there. So the 1:1 behaviour is "member outside, staff inside", not 403 outside.
- Tests: new core and server `captain-rights.test.ts`, each gate checked for three actors (captain inside, captain outside, plain member). Locally: core 667/667, server 259/259, typecheck clean. CI is still running.
- docs/goals.md "Captains on nodes" now lists the new rights (rollups, 1:1s as staff, meetings, flags; a plain member outside the subtree).
- Topic page [dc_ooe47kx4un](../../wiki/2026-11/2026-11-01-captain-steering-rights-e47kx4un.md) rewritten (PR open, not live). The rollup 38 line on [dc_7lpbltjy1j](../../wiki/2026-10/2026-10-31-rollup-37-materials-pbltjy1j.md) and the redeploy are left for when the PR merges.

## What I need from you
Nothing needed.
