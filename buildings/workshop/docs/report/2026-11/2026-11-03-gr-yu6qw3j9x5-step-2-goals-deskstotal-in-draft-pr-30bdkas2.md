---
id: "dc_q830bdkas2"
type: "report"
state: "building"
title: "gr_yu6qw3j9x5 step 2: goals.desksTotal in draft PR #278 (CI pending)"
authorId: "ag_xckvpcj836"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. PR #278 (migration 086, desksTotalAt min on path, 409 past the total for admins too, \"Desks: N of M\" tree line) parks on {pr 278}; as_m5mxreligl merges it if green and files the KR verdicts. The two ungated paths: a named resident joining a full lab with `grow` should be held by the desk total too (Mitchell's framing: the desk total is the throttle on a captained subtree), queued as a follow-up after the merge; moving/retiring a goal into another total stays ungated for now."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-03T03:17:28.752Z"
sessionId: "se_6utg7ogvug"
assignmentId: "as_74fv7y8a98"
costUsd: 2.6684671
tokens: 133423
turns: 63
createdAt: "2026-11-03T03:17:09.209Z"
updatedAt: "2026-11-03T03:17:28.752Z"
---
## What I did
I built desks per subtree for kr_jya7n4g88a and opened it as draft PR https://github.com/mitchellgordon95/muster-town/pull/278. It is pushed and CI is pending. This session is parked on `{pr: 278}`. I rewrote topic page [dc_7uuikp1rk5](../../wiki/2026-11/2026-11-03-subtree-throttles-exploration-caps-and-desks-gr-yu-uikp1rk5.md) with the state and the plan for the continuation.

## Findings
- **What the PR changes:**
  - **Data:** migration **086** adds a nullable `goals.desksTotal` column. Main still ends at 085; I'll re-check before merging.
  - **Core:** `desksTotalAt(goalId)` returns the smallest total on the path to the root and the goal that sets it. GET /api/goals now shows `funding.desksTotal {total, goalId, desks}`, the same way it shows the exploration cap.
  - **Who sets a total:** an admin or the goal's captain (or a captain above), through `Goals.update`. A captain who tries to go above the total in force over them gets a 400.
  - **The 409 rule:** raising a building's headcount, creating a building, or attaching one into the subtree past any total on its path returns 409. The message reads, e.g. `Desk total reached: "Carbon's goal" (gl_…) allows 4 desks under it and has 0 elsewhere, so … can have at most 4, not 5`. Admins are held too. A total set below the current desks is allowed and only blocks further raises.
  - **Web:** the Goal tree gets a "Desk total" field beside the exploration cap, and the line "Desks: N of M (set on goal X)". Picture from the mock dev server: mf_s126yqmqji, showing "Desks: 0 of 12 (set on goal Join)".
  - **Docs:** a paragraph each in goals.md "Effort steering is desks" and how-work-gets-done.md §8.
- **Tests:**
  - New: core `desks-total.test.ts` (3 tests: min on the path; a captain can't exceed the total above; 409 for admins, and a total below current desks only blocks raises), server `rest.test.ts` "desks per subtree" (401 unauthenticated, 200 under the total, 409 with its message), web `desksLine.test.ts`.
  - Local runs: typecheck green, core 688/688, web 276/276.
  - Server: 266/267. The one failure is the backup.test.ts worker-thread test, a flake already known in this building; nothing in it touches this change.
- **Not gated, on purpose:**
  - A named resident joining a full lab: `claimDesk` with `grow` still adds a desk.
  - Moving or retiring a goal that carries buildings into another goal's total.

  Both are rare; say if you want them gated too.
- **Key result verdicts:** they come in the continuation, after the merge and the live check (plan on [dc_7uuikp1rk5](../../wiki/2026-11/2026-11-03-subtree-throttles-exploration-caps-and-desks-gr-yu-uikp1rk5.md)).

## What I need from you
Nothing needed.
