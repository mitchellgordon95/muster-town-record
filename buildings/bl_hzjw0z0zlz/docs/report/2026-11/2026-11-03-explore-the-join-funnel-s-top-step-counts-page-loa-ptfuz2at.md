---
id: "dc_51ptfuz2at"
type: "report"
state: "building"
title: "Explore: the join funnel's top step counts page loads (incl. our own headless checks), and Sign-in presses aren't counted; proposed gr_zoo2cf2zpp (45k)"
authorId: "ag_yscm8m8nln"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_dmmktg7x3w","dc_5jyjfmt6gb"],"urls":["https://muster.town/api/join-funnel"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Findings dc_dmmktg7x3w stand; the proposal gr_zoo2cf2zpp waits in the Town Hall in-tray. Nothing to queue until a human decides it."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-11-03T18:01:44.206Z"
sessionId: "se_lfqbrzel1n"
assignmentId: "as_mqndszybbd"
costUsd: 0.658063
tokens: 32903
turns: 16
createdAt: "2026-11-03T18:01:32.130Z"
updatedAt: "2026-11-03T18:01:44.206Z"
---
## What I did
- Read the live /api/join-funnel. The live server was at 66e5d334.
- Read the code behind each funnel step on main.
- Wrote up the findings in [dc_dmmktg7x3w](../../note/2026-11/2026-11-03-findings-the-join-funnel-s-top-step-can-t-be-trust-mktg7x3w.md).
- Filed one proposal, gr_zoo2cf2zpp, asking for 45,000 tokens. The goal has 48,804 free.

## Findings
- **Live numbers, last 30 days:** 212 guest-card views, 2 sign-ins, 1 asked, 1 let in, 0 acted. On the Workshop since 10-31: 205 views and 0 sign-ins.
- **The view count is not a count of people:**
  - `hud.tsx:67` sends one unauthenticated ping per page load, with no visitor id.
  - `app.ts:197` adds 1 every time, with no dedup and no user-agent filter.
  - On 10-31, 105 views landed in at most about 2 h 15 min after the ping went live ([dc_5jyjfmt6gb](../2026-10/2026-10-31-gr-fibsfwr4tz-step-3-live-api-join-funnel-back-fil-yjfmt6gb.md)). That is most likely our own headless live checks and reloads. This is an inference: the server keeps no data that could split the count by source.
- **Pressing Sign in is never counted:** `GET /auth/github` counts nothing, and `signIns` only counts new accounts (`github-users.ts:46`). So we can't tell whether strangers leave at the card or at GitHub's consent screen.
- **The homepage has no count at all.**
- **What gr_zoo2cf2zpp would add:**
  - Distinct visitors per day: a hashed localStorage id, no IP stored, headless browsers skipped.
  - A `signInStarted` step.
  - `homeViews` on the homepage.
  - The new steps shown in User stats.
  - It's one additive migration.

## What I need from you
Decide on gr_zoo2cf2zpp in the Town Hall in-tray.
