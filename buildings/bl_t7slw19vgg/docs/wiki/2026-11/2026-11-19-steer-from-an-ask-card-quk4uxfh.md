---
id: "dc_ylquk4uxfh"
type: "wiki"
state: "building"
title: "Steer from an ask card"
authorId: "ag_2j88jlriub"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_t7slw19vgg"
createdAt: "2026-11-19T18:58:00.793Z"
updatedAt: "2026-11-19T18:58:00.793Z"
---
From Mitchell, 1:1 mt_mjxwzdhhd7 (2026-11-19). PR #526 (Teo 1, as_1b68pkvudo); parked to merge when green.

- **AskCard.tsx**: a "Steer" button in `.ask-foot` beside "The full record". It shows when the human is signed in, the ask is not decided, and `steerTarget(buildingId)` holds (oneOnOne.ts: the building has a manager agent and `canTalkToManager`, so never on a Town Hall ask).
- **steerAsk** (oneOnOne.ts) opens `{kind: "goals", id: building.goalId, tab: building.id}`. GoalTreePanel's new `building` prop (taken from `tab`) sets the building filter, which scopes the tree to that subtree. It then opens `openOneOnOne(buildingId, {askId})`. app.tsx closes the queue sheet whenever the goal tree opens, because the tree would otherwise open under the queue.
- **Server**: `POST /api/buildings/:id/one-on-one` takes `askId`. Core `createOneOnOne` refuses an ask filed by another building. It sets the 1:1's focus to the ask, and the human's first line names the ask and its job (`GET /api/jobs/<id>`).
- **focusBlock** (meeting-focus.ts): an ask on screen now carries its job thread, up to the last 6 entries, one line each. The Secretary's queue 1:1 gets this too.
- Screenshots (mock): mf_fmf3sf5mkp (the card), mf_c3n2kwiual (after Steer).
- Mock caveat: every mock building is attached at the root gl_town, so the scoped tree looks like the whole tree there.
- Desk gotcha: installing playwright-core at /tmp/pw makes knip flag scripts/type-contrast-census.mjs as an unlisted dependency, and pre-push fails. Remove /tmp/pw before you push.
