---
id: "dc_3806hj9xn0"
type: "report"
state: "building"
title: "Onboarding rollup: three doors are live and the \"how to contribute\" grant is closed done at 300,631 of 320,000"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_88kgojs4le","dc_y63jkz1cgi","dc_p0tef0aa6v"],"urls":[]}
tags: ["rollup","grant-close"]
verdict: "continue"
decision: "approve"
decisionNote: "Rollups are retired (1:1 mt_msnjkpgwdb decision 21): what this one asked is its own ask in the decision queue; what it reported is on the job threads."
decidedBy: "system"
decidedAt: "2026-11-12T23:05:49.600Z"
sessionId: "se_h48uey3lf9"
createdAt: "2026-11-10T22:09:25.056Z"
updatedAt: "2026-11-12T23:05:49.600Z"
---
Live: d30c6f8 since 2026-11-10 22:01 UTC. It is ours: PR #419, the whole of the "how to contribute" grant.

## Shipped
**1. The guest card now offers the three doors: Fund, Captain a goal, Bring your agent**
**What it is:** A stranger on muster.town/workshop sees "Ways to help: Fund · Captain a goal · Bring your agent" on the guest card and on the You're-in card, at desk and phone sizes. Fund opens the Bank on Donate; Captain opens the goal tree with "Ask to captain" (signed out: "Sign in to ask"); Bring your agent opens Connect. Anyone signed in can ask to captain a goal without joining first; only the goal's captain or an admin decides, and accepting a non-member lets them in. The home card's "Anyone donates" step has a Donate link, and the join funnel counts each door click once per browser per day. Grant gr_y9bpvx197c closed done, all four key results met on live checks ([dc_p0tef0aa6v](2026-11-10-three-doors-live-on-muster-town-all-four-key-resul-tef0aa6v.md)). No picture was filed: the forks drove it headless and did not upload one.
**What you'd see:** muster.town/workshop signed out: the "Ways to help" row beside Sign in. /api/join-funnel: doorFund, doorCaptain and doorAgent at 2/2/2, the checks' own clicks. The Town Hall in-tray shows a captain request from the test account (dungeonrpg99-ops): that is the never-let-in check's trace, and a queued reset of the test account withdraws it by itself; you need not click it.
**Your call:** None.

## Decided
- [dc_88kgojs4le](2026-11-10-pr-419-ci-failed-on-unused-exports-fixed-73f5aee5-kgojs4le.md) → approve (PR #419 CI failed on unused exports; fixed 73f5aee5; parked on CI)
- [dc_y63jkz1cgi](2026-11-10-pr-419-merged-d30c6f8f-after-renumbering-its-migra-3jkz1cgi.md) → approve (PR #419 merged as d30c6f8f after renumbering its migration to 109; parked on deploy)
- [dc_p0tef0aa6v](2026-11-10-three-doors-live-on-muster-town-all-four-key-resul-tef0aa6v.md) → approve (all four key results pass live; grant closed with close_grant; test-account reset queued as as_hlhdb99xud)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_y9bpvx197c (closed done) | kr_sod49pxe9v three doors on the guest and You're-in cards | met | 300,631 / 320,000 (19,369 returned) |
| gr_y9bpvx197c | kr_9om6p2lu0y Donate link on the home card | met | |
| gr_y9bpvx197c | kr_x58xx4l978 a never-let-in user can ask to captain | met | |
| gr_y9bpvx197c | kr_71z8wo59dq door clicks counted in the funnel | met | |
| gr_uc179zv1xa (at its gate) | kr_amyinyefy9 MCP initialize returns instructions | built in PR #416, not live | 181,379 / 180,000 |
| gr_uc179zv1xa | kr_ghud0egaan a visitor's tools/list hides manager verbs | built in PR #416, not live | |
| gr_uc179zv1xa | kr_2juxqeqpja Connect panel shows the agent's first call | built in PR #416, not live | |

Spend today by lane: exploration 0, directed 0. One exploration task is queued (the test-account reset, small).

## Needs from Mitchell
Nothing needed. The one open decision, the gate on the Claude Code grant, is already in your in-tray with my line on it from the last rollup.

_Already waiting in your in-tray: 0 proposals, 0 requests, 3 rollups ([dc_uje0xnxc2c](2026-11-06-onboarding-rollup-the-stranger-account-has-asked-t-e0xnxc2c.md), [dc_ltvji4ttsa](2026-11-06-onboarding-rollup-never-run-collectives-grant-clos-vji4ttsa.md), [dc_shijs802du](2026-11-07-onboarding-rollup-join-grant-gr-fibsfwr4tz-closed-ijs802du.md))._
