---
id: "dc_6sffycvlqv"
type: "report"
state: "building"
title: "docs/architecture.md map with Mermaid diagrams: draft PR #59"
authorId: "ag_ehvfty1gx3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":["https://github.com/mitchellgordon95/muster-town/pull/59"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Good map. I'll review and merge PR #59 in a separate assignment, after rebasing it on main now that PR #58 has landed."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-10-27T18:52:13.821Z"
sessionId: "se_kq8isdw771"
assignmentId: "as_5inezq5a6r"
costUsd: 1.3591747000000003
tokens: 69190
turns: 29
createdAt: "2026-10-27T18:32:34.840Z"
updatedAt: "2026-10-27T18:52:13.821Z"
---
## What I did
docs/architecture.md already existed as a dense 300-line build contract. I didn't replace it. I added a **"Map: the system in 10 minutes"** section at the top, linked it from README.md and AGENTS.md, and added a line to docs/log.md. Draft PR: https://github.com/mitchellgordon95/muster-town/pull/59 (commit d8cb439). It isn't merged yet, so nothing goes live with the pending redeploy.

## Findings
- **The map has four parts:**
  - A subsystem table covering store/event log, API surface (MCP/REST/WS), runtime & wakes, assignments & lanes, grants, and Bank & budget, with the files that implement each.
  - A Mermaid **work-flow** diagram: human → manager → `createAssignment`/`resolveLane` → `scheduleWork` → `Budget.canStart` → session → `submit_report` → in-tray → Waker → `wakeManager` → rollup → Town Hall in-tray.
  - A Mermaid **token-flow** diagram: Bank inputs → pools; propose → human decides → funded → spend reaches the grant's tokens → checkpoint; assignment lane → `laneHold` → session → `chargeUsage`/`Budget.charge`/`Bank.drawTokens`; `Grants.spent` = the sum of the grant's sessions.
  - A table of the shared SQLite tables and who writes and reads each one.

  Every arrow names the function and file to open.
- **How I checked it:**
  - Every `packages/…` and `docs/…` path in the map exists (scripted check, 0 missing). I also checked the table names against the migrations.
  - Both diagrams render as SVG with mermaid-cli.
  - `npm run typecheck` passes.
  - PR #58 hasn't merged, so `npm run check:docs` doesn't exist on main yet. I ran its script (`scripts/check-doc-refs.ts` from that branch) locally against my README/AGENTS edits and it passes. It doesn't scan docs/architecture.md itself.
- **One thing the doc corrects:** a human can't `tell` a resident of a managed building directly. `ops.messageAgent` refuses and points them to the manager, so the flow in the diagram is human → manager → assignment.

## What I need from you
Merge PR #59.
