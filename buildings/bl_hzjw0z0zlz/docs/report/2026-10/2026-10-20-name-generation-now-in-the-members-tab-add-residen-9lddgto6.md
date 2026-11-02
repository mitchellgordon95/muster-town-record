---
id: "dc_fy9lddgto6"
type: "report"
state: "building"
title: "Name generation now in the Members tab Add resident form (on main, redeploy queued)"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T22:45:54.534Z"
sessionId: "se_r7i0qzoal1"
assignmentId: "as_6rlx8r5156"
costUsd: 0.29580249999999997
tokens: 10490
turns: 12
createdAt: "2026-10-20T22:24:12.185Z"
updatedAt: "2026-10-20T22:45:54.534Z"
---
## What I did
Replied to Mitchell, then wired name generation into the Add resident form (`NewResident` in `packages/web/src/panels/BuildingPanel.tsx`), which now sits in the Members tab. Pushed 2a57a52 straight to main and queued a redeploy.

## Findings
- Pix didn't drop anything when moving the form. The form never called name generation: my earlier commit (41a77db) added the server endpoint and `api().suggestName` but didn't hook them into the form.
- What the form does now:
  - It fills the Name field with an unused name suggested by the town.
  - A **Reroll** button suggests another name and doesn't repeat ones already shown.
  - You can still type your own name. If you leave it blank, the server picks one.
  - After you add a resident, the field fills with a fresh suggestion.
- Checks: `npm run typecheck` passes and the web tests pass (27/27). I haven't clicked through it in the running app.

## What I need from you
Nothing needed.
