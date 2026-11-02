---
id: "dc_bjt8spgcdu"
type: "report"
state: "building"
title: "Waterfall step 1 (core) on main (ca5bd27): no review-policy setting, managers' reports and rollups go to the Town Hall in-tray; §3.1/§3.2 rewritten; steps 2–4 assigned to Root and Lena"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_g9d74v8kdb","dc_tizv52ml8n","dc_2i93rukmeq","dc_k955hun6c4"],"urls":["https://github.com/muster-town/agent-town/commit/ca5bd274dc7555d34abdda6c1805a21a52ffb7e2"]}
tags: []
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-24T23:15:19.171Z"
sessionId: "se_5uzy0qkiue"
assignmentId: "as_4fdtyhw7xu"
costUsd: 11.5816468
tokens: 335344
turns: 103
createdAt: "2026-10-24T21:34:22.141Z"
updatedAt: "2026-10-24T23:15:19.171Z"
---
## What I did
- Rewrote docs/waterfall.md §3.1/§3.2 (plus §2, §3.5, §5, §6) to Mitchell's four amendments and updated the town copy [dc_g9d74v8kdb](../../article/2026-10/2026-10-24-design-note-the-waterfall-goal-directed-budgets-re-d74v8kdb.md) from it.
- Built step 1 (core) and pushed it straight to main as ca5bd27 (CI deploys it; live was 386b654 when I pushed). Typecheck green in every package; core 237/237, runtime all pass, server 66/66 (two tests that timed out under desk load pass when re-run alone).
- Assigned, all gated on this assignment finishing so they fork from a main that has step 1: Root as_kduig68s47 (step 2, the manager's team-lead session), Root as_srwcoyr6qt (step 4, the 1:1), Lena as_608ywo4mk9 (step 3, Town Hall in-tray in the web).
- Found and killed an orphaned duplicate of my own session (started 20:05, before the server restart, same token and assignment) that was about to push its own version of step 1 from a second worktree (local branch pix-step1-core in ~/work/pixwt). I took two small pieces from its commit (the collective.json cleanup and resending the Town Hall count on grant events); the rest is mine. Runtime "orphaned at restart" sessions keep running in the desk container with a live token: worth a fix (Kelly's docs/meetings.md §3.5 touches the same drain).

## Findings
- (a) No review-policy setting: migration 029 drops the column; `managerAgentOf(building)` (manager agent not stopped/banned/retired) works the in-tray, else a human. Stopping the manager hands the in-tray back. `auto` and `reviewer` are gone (never used, per Kelly).
- (b) The manager session is Root's step 2; core provides `managerIntrayBlock` (pending resident reports with their "needs" line, decision verbs, the four escalation criteria, the rollup rule with the last rollup's time), appended to the manager's team block in every manager session. The runtime's per-report reviewer session (`maybeReview`) is deleted rather than kept as an interim.
- (d) Resident reports in a building with a manager agent notify agents only; the HUD shows in-tray notices only for in-trays a human works plus the Town Hall. Manager reports (rollups via `submit_report rollup: true` with covered reports in sourceIds, checkpoints, escalations, replies to "Message from Mitchell") are Town Hall in-tray items; `GET /api/buildings/town-hall/intray` returns `{ reports, grants }` with grants proposed/countered/checkpoint; `review` refuses an agent deciding its own report.
- Gap until step 2 lands: the Workshop's in-tray (manager = me) is worked by nobody automatically and the HUD no longer notices it; Mitchell can still walk to it. Root's and Lena's step reports will wait there.
- The `intray:town-hall` place and the Town Hall panel rows are Lena's step 3; today the Town Hall count appears on the building and the plain IntrayPanel can already list rollups.

## What I need from you
Nothing needed.
