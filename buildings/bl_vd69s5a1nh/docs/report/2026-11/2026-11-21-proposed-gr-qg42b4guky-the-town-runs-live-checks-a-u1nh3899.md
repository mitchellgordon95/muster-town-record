---
id: "dc_2du1nh3899"
type: "report"
state: "building"
title: "Proposed gr_qg42b4guky: the town runs live checks after a deploy (14% of work sessions only check the live site)"
authorId: "ag_buyu00ldh7"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Taken in. gr_qg42b4guky (M+S+S) is proposed with its ask card already filed; it reaches Mitchell in the decision queue on its own, nothing for me to render. Findings dc_1qha5spcyd stand on their own. Side finding on 1:1 sessions cut by restart passed to Prod."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-21T00:04:22.029Z"
sessionId: "se_ilkgj64f2d"
assignmentId: "as_0t0792byb0"
costUsd: 1.9570645999999996
tokens: 97853
turns: 41
createdAt: "2026-11-21T00:03:52.357Z"
updatedAt: "2026-11-21T00:04:22.029Z"
---
## What I did
Exploration as_0t0792byb0. I built on journal line 2026-11-19 [dc_8zvfwxreid](2026-11-19-proposed-gr-rlt0ctnhqk-the-town-merges-green-prs-i-vfwxreid.md) (merge-when-green): same method, the next mechanical class of session. I sorted the last 200 sessions (GET /api/sessions, 2026-11-19 02:30Z to 11-21 00:00Z) by assignment title, read core waits.ts and ask-checks.ts on main 9ba1f937, and filed findings [dc_1qha5spcyd](../../note/2026-11/2026-11-21-findings-14-of-work-sessions-only-check-the-live-t-ha5spcyd.md). Then I proposed gr_qg42b4guky (M+S+S, 250k) with its ask card.

## Findings
- There were 121 work sessions, which spent 5.82M adjusted tokens. 17 of them (14%, 479k tokens) only checked the live town after a deploy. About 7 of those 17 were plain HTTP or API reads: /api/directory empty, objectives route 404, pinger 200, og tags and robots.txt, a cap or a count read through the API. About 5 needed a screenshot.
- The server can already run these checks. ask-checks.ts has `url` and `api` runners and `verifyKeyResult` (event kr.verified). waits.ts already closes `{pr, merge:true}` work with no session. What is missing is a `{deploy, checks}` wait that runs those runners and closes the work. Expected saving: about 7 sessions and about 190k tokens per 2 days, ±50% because the window is only 2 days.
- Side note for Prod, not proposed: in the same window, 10 Secretary 1:1 sessions (344k tokens) were "cut by restart" during merge runs. The 8-min drain cannot end a 1:1.
- Not chosen: invariants docs. All 7 docs/invariants files were updated as recently as 11-17, so I found no clear gap there.

## What I need from you
Fund, counter or reject gr_qg42b4guky in the decision queue.
