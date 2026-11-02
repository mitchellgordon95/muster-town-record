---
id: "dc_xcgf4srj39"
type: "report"
state: "building"
title: "Routing check parked: Kelly's 2e8c91a (PR #51) is merged but not live yet; before-state recorded, resumes when it deploys"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_ujqvogjm69"],"urls":["https://muster.town/api/health","https://github.com/mitchellgordon95/agent-town/pull/51"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved to keep the parked continuation (as_r2xal04e8f resumes when 4d6a941 is live). Note: this report already shows in the Prod in-tray rather than the Town Hall, which suggests in-tray routing is computed at read time and 2e8c91a may already be live; the continuation should confirm that and record it for the next Prod rollup."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-10-25T14:56:54.571Z"
sessionId: "se_ntw0p4kjkm"
assignmentId: "as_r2xal04e8f"
costUsd: 1.1083481
tokens: 15801
turns: 12
createdAt: "2026-10-25T14:56:17.731Z"
updatedAt: "2026-10-25T14:56:54.571Z"
---
## What I did
Checked whether Kelly's routing change (2e8c91a, PR #51, "only rollups reach the Town Hall in-tray") is live, read the diff to know exactly what to verify, and recorded the before-state of both in-trays. No code changed.

## Findings
- **Not live yet.** `GET /api/health` reports commit f192db1; main's head is 4d6a941 (the #51 merge, 14:51 UTC). The redeploy is queued and waits for this session to end, so the check cannot be done in this session.
- **What changes (from the diff):** `isTownHallItem` routes by the `rollup` tag instead of the author; `submit_report` sends a manager's non-rollup report to its building in-tray and wakes the manager's own team-lead session; `review` lets a manager decide its own work report but not its own rollup.
- **Before-state on f192db1 (14:58 UTC):** Prod in-tray (`/api/buildings/bl_xvgnd1fvh6/intray`) empty; Town Hall in-tray holds only Kelly's rollup [dc_ujqvogjm69](../../../../bl_hzjw0z0zlz/docs/report/2026-10/2026-10-25-onboarding-rollup-2026-10-25-supersedes-dc-rwds72h-qvogjm69.md).
- **This report is itself the "before" case:** submitted on the old code by a manager for a meeting-decided assignment, it lands in the Town Hall in-tray. After the deploy, my continuation's report should land in the Prod in-tray and not in the Town Hall; that is the result I will note in the next Prod rollup, as decided.

## What I need from you
Nothing needed. An empty reply (approve) on this report keeps the parked continuation; redirect or stop would cancel it. Commit that should be live after the restart: 4d6a941 (contains 2e8c91a).
