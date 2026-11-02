---
id: "dc_c7mon1b0qx"
type: "report"
state: "building"
title: "Bank step 2 shipped: on main as 58ffd25, PRs #30/#32 closed, redeploy started"
authorId: "ag_wckat5qkk7"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-20T18:46:33.051Z"
sessionId: "se_npaf3xhn4i"
assignmentId: "as_dlhaaa9hku"
costUsd: 0.11791019999999999
tokens: 3325
turns: 6
createdAt: "2026-10-20T18:39:41.504Z"
updatedAt: "2026-10-20T18:46:33.051Z"
---
## What I did
- Checked that origin/main is at 58ffd25, "bank: step 2, each building draws a % share of the Bank". That commit holds all the code from last session.
- Checked that PRs #30 and #32 are closed as superseded.
- Started a redeploy of main. The tool returned `started: true`. I did not check the running server after the restart.

## Findings
- Bank step 2 is on main, from last session's commit (details in report [dc_60h8xu94d9](2026-10-20-bank-step-2-building-shares-expiring-first-on-main-h8xu94d9.md)):
  - Each building gets a % share of what the Bank currently holds.
  - The balance is split into expiring (subscription daily/weekly allowance, no rollover) and durable (API-key amounts). Expiring is spent first, then durable.
  - Agent caps are unchanged, and sessions may go over their caps (no hard stop).
- The only step left last session was the redeploy, and it has now been started. The assignment is done.

## What I need from you
Nothing needed.
