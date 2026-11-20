---
id: "dc_xkrp6svndd"
type: "report"
state: "building"
title: "Exploration: proposed showing how much incoming credit goes unused (gr_z13gmx54su)"
authorId: "ag_q0kdnqitaz"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Exploration done: findings dc_kmqlcmbs5u filed, gr_z13gmx54su proposed. Rendered its money ask for Mitchell."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-11-20T00:03:07.146Z"
sessionId: "se_1y8357zcjh"
assignmentId: "as_ymhzj3dgwd"
costUsd: 1.0110622
tokens: 50553
turns: 20
createdAt: "2026-11-20T00:02:26.108Z"
updatedAt: "2026-11-20T00:03:07.146Z"
---
## What I did
Read the live /api/finance, /api/finance/sources and /api/bank. Read the Balance tab signed out with playwright. Checked the code for gl_vjek98yym0's cache alert (already built: cache-miss.ts plus the HUD alert) and for goal spend (GoalSpend.tsx). Wrote findings [dc_kmqlcmbs5u](../../note/2026-11/2026-11-20-findings-most-subscription-credit-expires-undrawn-qlcmbs5u.md). Proposed gr_z13gmx54su under gl_5koas412u9: M+S = 200,000 tokens, two steps.

## Findings
- Over all time, 261,631,813 adj. tokens expired undrawn. That is 58% of the 453,833,333 ever credited.
- In the last 7 full days (11-13 to 11-19), 148,000,000 were credited and 24,672,835 used, which is 16.7%. Between 12.2M and 21.1M expired each day.
- The Balance tab shows "Net per day +17,894,144 / day surplus". Subscription credit does not carry over, so this is not real surplus. No sentence or chart gives the used share. Expiry appears only as an all-time row and per credit on Inputs.
- The proposal adds an expired count to each daily row, adds 7-day and 30-day used/expired sentences with a ✓ per-credit check, and rewords the surplus row. Three key results, kr_c0g8tvidke, kr_0ke5ezysx9 and kr_no6seja7f6, are due 2026-11-23. The town's estimate is 141k–193k for 3 similar grants.
- Not known: whether the weekly caps match the real plan limits. The used share is measured against credited tokens, not against real capacity.

## What I need from you
Render the money ask for gr_z13gmx54su (Fund, Counter or Reject).
