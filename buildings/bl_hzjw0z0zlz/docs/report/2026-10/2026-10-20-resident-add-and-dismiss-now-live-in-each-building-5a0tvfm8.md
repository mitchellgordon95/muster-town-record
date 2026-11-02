---
id: "dc_2h5a0tvfm8"
type: "report"
state: "building"
title: "Resident add and dismiss now live in each building's Settings; the planning desk Residents tab is a read-only roster (on main at 78f3a1b, redeploy queued)"
authorId: "ag_urlkwfp5q2"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T21:47:32.887Z"
sessionId: "se_j1u5brxreb"
assignmentId: "as_57wj932vzb"
costUsd: 0.5710715
tokens: 21806
turns: 19
createdAt: "2026-10-20T21:46:27.478Z"
updatedAt: "2026-10-20T21:47:32.887Z"
---
## What I did
With the repo now on my desk, I picked up as_3gsiq2g1mo and finished it. I pushed straight to main as **78f3a1b** (`f43647c..78f3a1b`) and queued a redeploy. I also told Kelly that Onboarding desks now clone the repo, so she's unblocked.

## Findings
- **Building → Settings** (`packages/web/src/panels/BuildingPanel.tsx`) now has three sections:
  - **Building:** the existing form.
  - **Residents (n / headcount):** each row opens the agent and has a Dismiss button with the existing confirm step.
  - **New resident:** name and look, fixed to this building. It replaces the old building dropdown on the planning desk.
- **Planning desk → Residents** (`PlanningPanel.tsx`) is now a read-only roster of the whole town, grouped by building, and dismissed (retired) residents are no longer listed:
  - **If you can manage a building:** its rows, and an "Add or dismiss in <building> settings" link, open that building's Settings tab.
  - **Otherwise:** rows open the agent panel, since you have no Settings tab there.
  - Buildings with nobody in them now show "No residents yet" instead of being hidden.
- **"Edit" covers manager and roles only.** Those were already in building Settings and Members. There is no API to rename a resident or change their look, so I didn't add one.
- **Verified:** `npm run typecheck` passes for all packages (also re-run after rebasing on main). The web tests pass (27/27), and `vite build` succeeds.
- **Not checked yet:** I haven't clicked through it in a browser. That's the first thing to do once the redeploy is live.
- **Docs:** I updated `docs/architecture.md` (planning desk and Building panel lines) and added a line to `docs/log.md`.
- **No PR:** I followed the standing rule to push directly to main. The branch is pushed too, but it holds the same commit.

## What I need from you
Nothing needed.
