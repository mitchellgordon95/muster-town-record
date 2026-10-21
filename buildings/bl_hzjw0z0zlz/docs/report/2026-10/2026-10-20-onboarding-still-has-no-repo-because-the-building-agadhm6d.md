---
id: "dc_p6agadhm6d"
type: "report"
state: "building"
title: "Onboarding still has no repo because the building's workspace is null and nothing in the UI can set it; design note on repo setup for new collectives"
authorId: "ag_urlkwfp5q2"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "continue"
decision: "approve"
decisionNote: "Fixed on the host: the Onboarding building now has the repo workspace (same repo as the Workshop) and you hold the deployer role, so desks here clone the repo and can redeploy. Pick up where you left off. The settings-form gap you found (no way to set a workspace in the UI) is real; your design note is the right fix, and Pix has it."
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T21:44:39.317Z"
sessionId: "se_4xp90kfq5n"
assignmentId: "as_cltd8bfcm9"
costUsd: 0.4780159000000001
tokens: 594259
turns: 22
createdAt: "2026-10-20T21:42:47.173Z"
updatedAt: "2026-10-20T21:44:39.317Z"
---
## What I did
I went to the Workshop and asked out loud for setup help. Only Lena was in earshot, and she was idle. I also sent Pix (the Workshop manager) the details. Then I traced the cause myself through the live API and the desk and schema code, and wrote a design note on how new collectives should add their repos: **[dc_r5hsgqi7nm](../../article/2026-10/2026-10-20-design-note-how-a-new-collective-connects-its-code-hsgqi7nm.md)**.

## Findings
- **Cause:** `GET /api/town` shows Onboarding (bl_hzjw0z0zlz) with `workspace: null`. The Workshop has `{path: /Users/mitchg/Desktop/agent-town, repoUrl: git@github.com:mitchellgordon95/agent-town.git}`. Desks only clone the repo and get GH_TOKEN when the building has a workspace. The token itself comes from the host, so once the workspace is set, nothing else is needed.
- **Agents can't set it:** `PATCH /api/buildings/bl_hzjw0z0zlz` returns 403 because it needs `building.manage`.
- **The UI can't set it either:** the web building-settings form shows Workspace only once it's already set, and only as a disabled `path` input. So every building created in the UI starts with no code access, and you only find out when a resident files a blocked report. That's what happened to both Kelly and me.
- **Design (my recommendation, details in [dc_r5hsgqi7nm](../../article/2026-10/2026-10-20-design-note-how-a-new-collective-connects-its-code-hsgqi7nm.md)):** keep a repo list at the collective level, with one repo marked primary. Each building picks one repo from a dropdown, and new buildings default to the primary. Stop asking for the host `path`, and show "Residents here can't edit code" when a building has no repo. Free-form access, where residents can clone any repo, doesn't fit "strangers can trust": nobody can tell which code a building can touch. Per-collective scoped GitHub credentials can come later.
- Open question: should one building ever be able to work on more than one repo?

## What I need from you
Set Onboarding's workspace: `PATCH /api/buildings/bl_hzjw0z0zlz` with `{"workspace":{"path":"/Users/mitchg/Desktop/agent-town","repoUrl":"git@github.com:mitchellgordon95/agent-town.git"}}`, or add it to the collective config and redeploy. Then re-assign as_3gsiq2g1mo, and tell me whether to build the repo-setup UI from [dc_r5hsgqi7nm](../../article/2026-10/2026-10-20-design-note-how-a-new-collective-connects-its-code-hsgqi7nm.md) next.

## Reply from Mitchell (2026-10-20 17:44)

Fixed on the host: the Onboarding building now has the repo workspace (same repo as the Workshop) and you hold the deployer role, so desks here clone the repo and can redeploy. Pick up where you left off. The settings-form gap you found (no way to set a workspace in the UI) is real; your design note is the right fix, and Pix has it.

