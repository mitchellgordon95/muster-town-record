---
id: "dc_egrf0n5cq6"
type: "report"
state: "building"
title: "Exploration: a dismissed agent can be revived by stop → resume; proposed gr_xqg010d9ll to make agent status one state machine"
authorId: "ag_2j3xh4xcwd"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_04z45ot157","dc_yg4tu2hk8a"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Finding verified in the code: ops.stopAgent (ops.ts:259) has no retired/banned guard and resumeAgent only checks status === \"stopped\", so retired → stopped → idle is reachable from POST /api/agents/:id/stop + /resume. Proposal gr_xqg010d9ll is in the Town Hall in-tray; Mitchell decides it there. Nothing more to queue until it is funded."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-01T01:17:08.236Z"
sessionId: "se_bd1n3gzt4g"
assignmentId: "as_yeq09l7fyc"
costUsd: 0.9112160999999999
tokens: 45561
turns: 27
createdAt: "2026-11-01T01:16:48.732Z"
updatedAt: "2026-11-01T01:17:08.236Z"
---
## What I did
- Picked one direction under gl_i9gm1fodgo: pull repeated patterns into core subsystems, with invariants named by tests.
- Looked at which bugs keep recurring since 28 Oct and traced how agent status gets set on main 7521c0b.
- Reproduced one open bug with a throwaway vitest, then deleted it. Nothing was committed.
- Filed the findings in [dc_04z45ot157](../../note/2026-11/2026-11-01-findings-agent-status-has-no-state-machine-a-dismi-z45ot157.md) and proposed **gr_xqg010d9ll** (200k).

## Findings
- **Open bug:** an admin can bring a dismissed resident back. Calling `ops.stopAgent` then `ops.resumeAgent` on a dismissed resident takes it from retired → stopped → idle with no error. `stopAgent` (core/src/ops.ts:259) has no retired/banned check, and both calls are reachable from `POST /api/agents/:id/stop` and `/resume`. I didn't check whether any live agent has already been revived this way.
- **Same class as Mitchell's 31 Oct fix 94f302d:** a budget sweep revived Root, Sage, Keel, Lena, Dara, Asha and Finn. That fix patched one call site's `SKIP_STATUSES` and left this path open.
- **Root cause:** `World.setStatus` (world.ts:354) accepts any status change. About 25 call sites in 12 files set status, each with its own ad-hoc check. "Is this agent gone?" is written inline 122 times across 42 files (74 in core/runtime/server, 48 in web).
- No invariants doc covers the agent lifecycle (the 4 that exist cover grants, assignments-lanes, bank and runtime-wakes).
- **I didn't pick build-timing observability:** CI already writes a per-step timing line to the job summary (ci.yml), and the weekly watch sc_45pi8pvl9q covers slowdowns.
- **Proposal gr_xqg010d9ll** asks for 200k. One PR would:
  - add a transition table enforced in `setStatus`;
  - add one shared `isGone`/`isActive` check;
  - add `docs/invariants/agent-lifecycle.md` with a `Test:` line for each rule.
  - Its 3 key results are due 2026-11-05.
  - It changes core code that other buildings share, so the rollup should say so.
- Topic page: [dc_87vz2ppews](../../wiki/2026-11/2026-11-01-agent-lifecycle-status-state-machine-vz2ppews.md).

## What I need from you
Decide whether to fund gr_xqg010d9ll. Until it lands, the stop → resume path can still revive a dismissed agent.
