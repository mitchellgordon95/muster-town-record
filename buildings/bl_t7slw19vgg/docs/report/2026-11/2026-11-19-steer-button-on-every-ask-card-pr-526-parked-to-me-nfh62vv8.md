---
id: "dc_dpnfh62vv8"
type: "report"
state: "building"
title: "Steer button on every ask card: PR #526, parked to merge when green"
authorId: "ag_2j88jlriub"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-19T18:58:08.861Z"
sessionId: "se_9wn2ap9bke"
assignmentId: "as_1b68pkvudo"
costUsd: 2.8104797000000006
tokens: 140524
turns: 60
createdAt: "2026-11-19T18:58:08.854Z"
updatedAt: "2026-11-19T18:58:08.861Z"
---
## What I did
I built the Steer button Mitchell asked for in 1:1 mt_mjxwzdhhd7 and opened PR #526 (https://github.com/mitchellgordon95/muster-town/pull/526). It is parked to merge when green. Topic page: [dc_ylquk4uxfh](../../wiki/2026-11/2026-11-19-steer-from-an-ask-card-quk4uxfh.md).

## Findings
- **The card.** Every open ask filed by a building with a manager now shows a **Steer** button beside "The full record". A human sees it only if they may talk to that manager (`canTalkToManager`). Town Hall asks and decided asks have no Steer button.
- **Pressing Steer** closes the queue sheet. It opens the goal tree at the filing building's goal, with the building filter set so the tree shows only that subtree (new `building` prop on GoalTreePanel). It opens the human's 1:1 with the building's manager in the sidebar.
- **What the manager has in context.** `POST /api/buildings/:id/one-on-one` now takes `askId`. The human's first line presents the ask and its job (`GET /api/jobs/<id>`). The 1:1's focus is set to the ask, so each human line reaches the manager with the ask card in front of it. That card now includes the last 6 entries of the ask's job thread, one line each. The Secretary's queue 1:1 gets the thread lines too. An ask filed by another building is refused.
- **Screenshots** (mock town): the card with Steer is ![queue](/api/media/mf_fmf3sf5mkp.png); after pressing it is ![steer](/api/media/mf_c3n2kwiual.png). The second shows the goal tree scoped to Workshop and the 1:1 with Keel presenting the ask and its job. In the mock every building is attached at the root goal, so the scoped tree there looks like the whole tree.
- **Verification.** New core/test/steer-ask.test.ts, plus a Steer case in web askCard.test.tsx. All suites pass: core 1098, web 451, server 359. Typecheck and `check --fast` are green. I have not seen it live yet.

## What I need from you
Nothing needed.
