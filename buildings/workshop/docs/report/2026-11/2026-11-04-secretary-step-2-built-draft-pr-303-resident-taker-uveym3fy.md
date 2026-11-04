---
id: "dc_ppuveym3fy"
type: "report"
state: "building"
title: "Secretary step 2 built: draft PR #303 (resident, takerId, digest builder, retainer asked at boot); parked on CI"
authorId: "ag_cj4h5ygdmh"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Step 2 built as draft PR #303 (0cd68de); its merge+redeploy continuation as_gwuaxbg2mo waits on {pr:303}. Step 3 (web) queued waiting on that merge."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-04T16:22:19.759Z"
sessionId: "se_rsff0t7c87"
assignmentId: "as_diz0qzkpuz"
costUsd: 4.339739499999999
tokens: 216987
turns: 18
createdAt: "2026-11-04T16:22:05.364Z"
updatedAt: "2026-11-04T16:22:19.759Z"
---
## What I did
I built step 2 of gr_kdlogzzo5s as one draft PR: https://github.com/mitchellgordon95/muster-town/pull/303 (head 0cd68de). I did not touch Grants.decide or act_in_1on1. I folded in Pix's note: the Secretary's 1:1 brief now carries the exact ISO `at` of each of the human's lines. Topic page: [dc_t20pm17xh1](../../wiki/2026-11/2026-11-04-the-secretary-gr-kdlogzzo5s-0pm17xh1.md).

## Findings
- **Secretary resident** (core `secretary.ts`, `world.secretary`): a Town Hall resident titled "Secretary", beside the Planner. The Planner stays manager. The Secretary has no role. It is made idempotently at server boot (main.ts), so it **has no agent id yet**: it gets one on the first boot of this commit. The boot log prints it, or read `GET /api/buildings/town-hall/schedules` → `takerId`. A human opens a 1:1 with it from the Town Hall panel ("Talk to Secretary" next to "Talk to ★ Planner"). createOneOnOne accepts its agentId. Its 1:1 prompt says to act only on the human's words with "`act_in_1on1` if available". It also lists the in-tray's yes/no lines and the human's lines from the last 30 min, each with its exact `at`.
- **Schedules take `takerId`** (migration 088, additive; no other open PR uses 088). A run goes to that resident's own queue, on the schedule's model. The Town Hall now accepts a schedule only with a takerId. Own-queue assignments run on `assignment.model` when it is set (work.ts, desk session, Budget.sessionModel).
- **Digest builder**: `digestDecisions` builds yes/no lines from the review deck's data:
  - "Continue gr_x (…) with a 200k top-up (spent 410k of 600k; a top-up buys: …)?"
  - "Fund gr_y (…) at its 350k ask?"
  - goal proposals, captain asks and retainer asks, as yes/no lines
  - rollups' real Your calls
  - outbox requests as one "Asked of you" line
  
  A new verb `digest` (Secretary only) returns the inputs when called with no args. With `shipped` lines it files the card.
- **Digest doc shape (what web step 3 needs)**:
  - type `digest`, state building, buildingId `town-hall`, tags ["digest"]
  - provenance.sourceIds = the covered rollups
  - body sections: `## Decisions needed` / `## Shipped since last digest` / `## Covered rollups`
  
  Covered rollups that ask nothing are archived. **One change from the assignment:** a rollup with a real "Your call" stays pending, so archiving can't hide a decision; its call appears as a Decisions line. Step 3 should render the newest digest doc first, with live lines from `digestDecisions`.
- **The run**: the schedule "Daily in-tray digest" runs daily at 07:00 UTC, taken by the Secretary, lane retainer, 10,000 tokens per run, on the Town Hall's cheapModel. Its prompt is the schedule's description. Over the default 14 days that is about 140k tokens. It is created at boot with its retainer **asked**, so it reaches the Town Hall in-tray on the first deploy. **No schedule id yet**: it is made at that first boot. A due run is skipped before any session when no rollup came in or a card was already filed that UTC day.
- **Tests**: 6 new core tests in secretary.test.ts (takerId, Town Hall refusal, cheap-model run, skip, yes/no lines from fixtures, filing and archiving). The full `npm run check` passed except one server test, backup.test.ts "worker thread", which hit a 5 s timeout under load; rerun alone it passed 23/23.
- **Next session**: expect a merge conflict with #300 (both add a verb to the schema lists, verbs/index.ts and describe.ts).

## What I need from you
Nothing needed.
