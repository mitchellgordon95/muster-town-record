---
id: "dc_ayegd42q8w"
type: "report"
state: "building"
title: "Work routing map filed (dc_4xww7x920l): 21 paths create work; 13 can land on a forking manager's own queue, and PR #369 closes 3"
authorId: "ag_ybb7tazy97"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_4xww7x920l","dc_ktzj41hv8x","mt_peubjyoo0k","ms_umw503g41h","as_1id0gxxxyc"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/369"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Map dc_4xww7x920l filed and topic page dc_ktzj41hv8x written; Mitchell will bring it to a meeting. PR #369 (Workshop) covers holes A1–A3; the docs fixes (D1–D6, architecture.md) wait for that meeting."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-05T20:35:04.285Z"
sessionId: "se_3xbzb7zi7m"
assignmentId: "as_nsl61wwka7"
costUsd: 3.5940166000000007
tokens: 179701
turns: 53
createdAt: "2026-11-05T20:34:41.651Z"
updatedAt: "2026-11-05T20:35:04.285Z"
---
## What I did
Read every `createAssignment` call site and the tell relay, park, scheduler, fork-spawn and lane-gate code at main 83ce501. Checked them against docs/architecture.md, how-work-gets-done.md, wakes.md and invariants/assignments-lanes.md. Asked Pix about the narrow fix (they replied in ms_umw503g41h: PR #369) and read its diff. Filed the map as **[dc_4xww7x920l](../../article/2026-11/2026-11-05-work-routing-the-map-ww7x920l.md)** "Work routing: the map" (article, in our cabinet) and the topic page "Work routing" ([dc_ktzj41hv8x](../../wiki/2026-11/2026-11-05-work-routing-zj41hv8x.md)). No code changed.

## Findings
- **Why work ends up on a manager.** There are 21 paths that create work (table in [dc_4xww7x920l](../../article/2026-11/2026-11-05-work-routing-the-map-ww7x920l.md) §1, each with file:line and the test that names it). `createAssignment` sends work to the named agent's own queue by default (domain.ts:59). Work reaches the building queue only when the caller says so or when the named agent is a fork (domain.ts:62). The runtime starts managers' own-queue work as their own work session (runtime index.ts:602-620), and their in-tray waits until it ends (manage.ts:167).
- **Holes A: 13 paths can put work on a forking manager's own queue.** PR #369 (draft, CI pending) closes 3 of them:
  - meeting decisions (A1);
  - the same decisions also approving the manager's pending reports, rollups included (A2);
  - `review` continue/redirect on the manager's own report (A3).
- **It leaves the other 10:**
  - tell relays, mentions, request answers and amended-decision wakes (wakes.ts);
  - a human's `assign` with the manager as agentId, and POST /agents/:id/work;
  - a schedule whose `takerId` names the manager;
  - `retry` of a cancelled building-queue row (inferred, not run);
  - a flag with assigneeId = the manager (a test asserts this, so it is a rule);
  - a manager parking its own work (probably intended).
- **Live example from this session:** my one-line tell to Pix became as_1id0gxxxyc on Pix's own queue.
- **Other holes (B):**
  - `review`'s assigneeId is silently ignored on reports.
  - An outbox answer to a fork that has already retired wakes nobody (inferred).
  - Postmortems and reorg prep stall in a visitor-managed building (inferred).
- **Rules that live only in prompts (C):**
  - "managers do decisions and rollups only" (prompts.ts:412);
  - rollups at least 4 h apart (prompts.ts:298);
  - the desk brief says directed work is "never held for money" (prompts.ts:206), but the code holds it (lanes.ts:164-170).
- **Docs that disagree with the code (D1–D6):**
  - "Message from" assignments are documented as removed, but they are live;
  - the schedule taker rule in invariant 7 and the "one owner" rule in invariant 8 are stale;
  - how-work-gets-done §6 says directed work is never held;
  - the "Get human decisions" assignment no longer exists;
  - the family cap in architecture.md:278 is gone.
- **Manager-only jobs:** checkpoint and grant funded/countered/rejected (grants.ts:785, 817-861). Nothing marks them as manager-only; they stay on the manager only because their callers don't set a queue.
- **What docs/architecture.md now gets wrong** (for a docs session after the meeting):
  - the subsystem table row (:22) is missing the retainer lane and the two queues;
  - the work-flow diagram (:31-52) shows one creator, no building queue and no forks, and none of the system creators;
  - the text at :56-57, :98, :278 and :289-291 is stale.
- [dc_4xww7x920l](../../article/2026-11/2026-11-05-work-routing-the-map-ww7x920l.md) §4 has 6 questions a redesign would have to decide.

## What I need from you
Nothing needed.
