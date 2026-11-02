---
id: "dc_loqehjmgjd"
type: "report"
state: "building"
title: "Proposed gr_8i952perny: stop a funded grant (human-only, wind-down, refund, KRs missed, in-tray); 300,000"
authorId: "ag_848kp6n6q3"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Proposal gr_8i952perny filed per 1:1 mt_a6wb51enia D4; the brief shows it funded (500,000), so its first step comes as its own \"Grant funded\" assignment. The member-funded correction (rest stays on the member's input) is noted."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-02T03:29:59.344Z"
sessionId: "se_tquh7muvd8"
assignmentId: "as_8a5bywnqw0"
costUsd: 0.6212995000000001
tokens: 31065
turns: 15
createdAt: "2026-11-02T03:29:25.266Z"
updatedAt: "2026-11-02T03:29:59.344Z"
---
## What I did
Checked the stop path in the code at main 024b236 and wrote it up in [dc_dhhy0zoi52](../../note/2026-11/2026-11-02-findings-what-closing-a-funded-grant-as-stopped-do-hy0zoi52.md). Then filed the proposal **gr_8i952perny** on gl_join (findings [dc_7yr1fea9lc](../../note/2026-11/2026-11-02-findings-a-non-admin-captain-can-commit-the-shared-r1fea9lc.md) and [dc_dhhy0zoi52](../../note/2026-11/2026-11-02-findings-what-closing-a-funded-grant-as-stopped-do-hy0zoi52.md); ask 300,000) with 4 dated key results. I built nothing.

## Findings
- **Confirmed:**
  - A manager can close a funded or checkpoint grant as "stopped" (grants.ts l.476-489; the LIVE check at l.485 only blocks other outcomes).
  - Closing does no bookkeeping. The unspent rest stops being claimed right away, because free-tokens.ts l.66, lanes.ts l.145 and grants.ts l.288/467 only count funded and checkpoint grants.
  - Running forks are not touched and keep spending.
  - Queued grant-lane assignments stay "held: grant closed" for good (lanes.ts l.120).
  - Key results stay open. Only closeDone claims them; `close` and the checkpoint "cut" leave them as they are.
- **Correction:** a member-funded grant's rest does **not** go to the pool. Member funding reserves nothing ("Nothing is reserved", requireFundingInput). Sessions draw from the member's input as they run (budget.ts l.330 drawFromInput), so the rest just stays on that input.
- **Also found:**
  - Nothing goes to the in-tray. When a human closes a grant, the manager's wake says "…at its checkpoint" even when the grant wasn't at one (wakes.ts l.47-60).
  - When a manager closes its own grant, nobody is told.
  - The web has no stop or close button: api.ts closeGrant is never called from the panels.
- **Proposal gr_8i952perny:**
  - A new `POST /api/grants/:id/stop` needs building.fund. The manager's close as "stopped" is limited to withdrawing proposed or countered grants.
  - The grant first goes to an interim status, "stopping". Its live forks get stop_fork, its queued work is cancelled with the reason, and it closes once their reports land or the 5-minute hard stop passes.
  - The close records spent, granted and returned.
  - Open key results are marked missed with the reason.
  - The stop shows as a Town Hall in-tray row and a review-deck slide.
  - A "Stop grant" button on the web asks for a reason.
  - Key results are due 2026-11-06 to 11-08. The 300,000 ask is based on gr_zsm1piyqyx's core and server step (73,579), plus a web step with a live check, a migration and the fork-wait logic.

## What I need from you
Fund, counter or reject gr_8i952perny.
