---
id: "dc_yws5xx6a04"
type: "report"
state: "building"
title: "Draft PR #27: explicit building manager + ★ badge; why Pix was picked and why Sage was missing"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "merge"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T04:15:00.575Z"
sessionId: "se_ruf9ccaev6"
assignmentId: "as_rupsta983v"
costUsd: 1.7904939000000006
tokens: 138328
turns: 60
createdAt: "2026-10-20T04:12:23.517Z"
updatedAt: "2026-10-20T04:15:00.575Z"
---
## What I did
Read the facilitator and invite logic in `packages/core/src/meetings.ts` and the web attendee picker. Checked the live meetings and Sage's events through the town API. Then built an explicit manager setting with a badge and opened draft PR https://github.com/mitchellgordon95/agent-town/pull/27.

## Findings
- **How Pix got picked:** there was no setting. The Workshop has no reviewer agent, so `defaultFacilitator` used `attendees[0]`. Server defaults order residents by join time, and Pix is first in `collectives/workshop/collective.json`, so Pix facilitated 3 of the 4 standups. The 03:59 standup (mt_qw6pkmas93) was called from the UI picker. The picker sends invitees sorted by name, so the facilitator became Lena.
- **Why Sage was missing:** it wasn't a bug in how the invite list is built. Sage was `stopped` at 03:58:40, 22 s before that standup was called at 03:59:02. The picker drops stopped residents without saying so. Sage is still `stopped` now.
- **What the PR changes:**
  - New `Building.managerAgentId` field (migration 009), set in building Settings → Manager.
  - Only an active resident of the building can be manager, and only someone who can manage the building can set it.
  - Who facilitates: the manager, then the reviewer, then the first resident by join order (no longer whoever sorts first by name).
  - The manager gets a gold ★ on their map name tag, a "★ manager" pill in their agent panel, and a "Manager" role label.
  - The picker now lists stopped residents greyed out with their status.
- **Verified:**
  - `npm run typecheck` is clean.
  - `npm test` passes in all packages: 83, 20, 30, 26 and 10 tests. That includes 3 new core tests and 1 new web test. One existing migration test needed a matching column drop.
  - In a headless Chromium browser check on the mock UI, the agent panel showed the badge and Settings showed the Manager dropdown. I didn't see the map ★ on screen because the mock manager had walked out of view.

## What I need from you
Merge PR #27, then pick the Workshop's manager in Settings (nothing is set automatically), and resume Sage if they should be at standups.

## Reply from Mitchell (2026-10-20 00:15)

merge

