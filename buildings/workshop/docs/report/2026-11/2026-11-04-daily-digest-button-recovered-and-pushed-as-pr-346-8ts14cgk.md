---
id: "dc_vm8ts14cgk"
type: "report"
state: "building"
title: "Daily digest button recovered and pushed as PR #346 (2803c098); parked on CI"
authorId: "ag_9a1a2eb2vs"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. Stash recovered, PR #346 (2803c098) open; your parked continuation (as_l3k8lpk0dq, waiting on {pr: 346}) merges it when green and parks on the deploy. No redeploy per Prod's FYI."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-04T19:47:37.426Z"
sessionId: "se_brtaiac7aq"
assignmentId: "as_v20kp4okvx"
costUsd: 0.8040546
tokens: 40203
turns: 21
createdAt: "2026-11-04T19:47:22.721Z"
updatedAt: "2026-11-04T19:47:37.426Z"
---
## What I did
The last session's work was never pushed. I found it in local stash@{0}, which the desk saved automatically when it switched branches. I applied it onto current main and resolved two import conflicts: in core secretary.ts (kept main's STARTER_MANAGER_MODEL) and in the server's town.ts (kept main's AddBankFee/EndBankFee). I moved the new route so it no longer sat between the retainer route and its doc comment. I also added 5 words to the manual: 1898 of 1900 words, so the cap check passes. Pushed 2803c098 and opened PR #346 (marked ready): https://github.com/mitchellgordon95/muster-town/pull/346

## Findings
- **What it does:** a **Daily digest** button in the Town Hall in-tray header, next to Talk to Secretary. It calls `POST /api/digest/run` (core `pressDigest`), which gives the Secretary one digest run paid from the digest's retainer. That is the same prompt, model and card as the 07:00Z run, and it does not move the schedule's next run.
  - Who sees it: only a human who can decide that retainer. `GET /api/buildings/town-hall/intray` carries `digestRun`, which is null for everyone else.
  - When it is refused (button disabled, with the reason): while a run is under way, before the retainer is approved, or when no rollup has arrived since the last card.
  - The once-a-day limit now applies only to the schedule, so a press can file a second card the same day; the newest card goes on top.
- **Checks, run in the foreground:**
  - deadcode, typecheck and check:docs: clean.
  - Targeted tests: core secretary.test.ts 10/10, server digest-intray.test.ts 2/2, web talkToSecretary.test.tsx 4/4.
  - Full `npm run check`: one failure out of 288 tests, in backup.test.ts ("maxGap 116 < 100"), the timing flake Pix 4 also saw. Run alone it passes 23/23.
- **Next session:** when CI on #346 is green, merge it (no `redeploy`), name the merge sha and park on {deploy: sha}. Then check live: the in-tray as a guest has no `digestRun`, and the button only shows to a signed-in admin.

## What I need from you
Nothing needed.
