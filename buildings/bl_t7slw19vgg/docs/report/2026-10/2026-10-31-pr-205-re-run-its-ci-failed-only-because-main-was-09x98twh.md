---
id: "dc_m709x98twh"
type: "report"
state: "building"
title: "PR #205 re-run: its CI failed only because main was red; fixed main (PR #209), parked on #205's CI"
authorId: "ag_wswe5yv69w"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Good catch fixing main (#209, live in b295b39). Continuation as_y0p6j8um2i already waits on #205's CI to merge, redeploy and check the fountain town live."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-10-31T22:02:06.271Z"
sessionId: "se_33qpi3n9ko"
assignmentId: "as_i9vxfnelvj"
costUsd: 0.740492
tokens: 37025
turns: 25
createdAt: "2026-10-31T22:02:02.507Z"
updatedAt: "2026-10-31T22:02:06.271Z"
---
## What I did
- Found that #205's CI failure (f46c8c1) wasn't caused by #205. The failing test was `finance-fly.test.ts > sizes the town Machine as fly.town.toml does`, and main was failing it too after 48a7d53, which moved fly.town.toml to performance-1x while `TOWN_MACHINE` in core stayed at shared-cpu-2x.
- Opened PR #209 (https://github.com/mitchellgordon95/muster-town/pull/209): it sets `TOWN_MACHINE` to performance-1x and widens a type in the test. I left it for its owners to merge, but it was already merged by the time I checked (b295b39).
- Merged the latest main into #205 and resolved the docs/log.md conflict, giving head 20cf63c. Pushed it, and updated topic page [dc_004hyy29z6](../../wiki/2026-10/2026-10-31-town-layout-doors-on-any-side-the-planned-fountain-4hyy29z6.md).

## Findings
- While main is red, nothing goes live: CI promotes only a green main commit to `prod`. Between 48a7d53 and #209, no merge could deploy, including #207 (bubble basenames).
- `npm run check` passes locally on #205's exact head 20cf63c: docs, deadcode, typecheck and all tests (4m33s). CI on that head is running.
- #209 changes what the finance page's Hosting section reports for the town Machine: $33/month at performance-1x instead of $13.39 at shared-cpu-2x. That matches the size Mitchell set.

## What I need from you
Nothing needed. I resume when #205's CI finishes, then merge, redeploy and check the fountain town live.
