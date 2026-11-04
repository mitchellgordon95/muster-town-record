---
id: "dc_ma6lxs0r8d"
type: "report"
state: "building"
title: "Meeting subtitle in plain words: PR #292 open, waiting on CI"
authorId: "ag_u7xmcysw2c"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Acknowledged. The continuation (as_bmld67qua7: merge + redeploy when PR #292 CI is green) is already waiting on {pr: 292}; nothing more to queue."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-04T00:57:48.710Z"
sessionId: "se_9q722jr92i"
assignmentId: "as_5mj4qsubfa"
costUsd: 0.42675549999999995
tokens: 21338
turns: 12
createdAt: "2026-11-04T00:57:42.238Z"
updatedAt: "2026-11-04T00:57:48.710Z"
---
## What I did
Changed the meeting header subtitle so it shows the meeting kind in plain words instead of the slug. Opened draft PR https://github.com/mitchellgordon95/muster-town/pull/292 and parked it until CI finishes.

## Findings
- New `packages/web/src/panels/meetingSubtitle.ts` gives plain words for all 7 MeetingKind values (schema index.ts:1042): standup → Standup, retro → Retro, planning → Planning meeting, town-hall → Town hall meeting, one-on-one → 1:1, in-tray-review → In-tray review, ad-hoc → Meeting. It leaves out the building name when it's empty, and for town-hall meetings (where it would just repeat "Town Hall").
- `MeetingPanel.tsx:118` uses it. The 1:1 branch is unchanged because it never showed the slug.
- So "town-hall · Town Hall · facilitated by Planner" now reads "Town hall meeting · facilitated by Planner".
- Added test `packages/web/test/meetingSubtitle.test.ts`, which also checks that every kind has words and none is shown as its slug. Typecheck is clean and the web tests pass (290/290).
- Next session: when CI is green, mark the PR ready, merge, redeploy, and report the merge commit as the one that should be live.

## What I need from you
Nothing needed.
