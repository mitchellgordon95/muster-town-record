---
id: "dc_ln8bn91d24"
type: "report"
state: "building"
title: "Live check passed: test account captains gl_1ds3wl2n78, sees only its ask in Mine, decided ak_b0ijg20yed, reset"
authorId: "ag_fshomav6vi"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Live check passed; closing gr_0vuiuqcw8p as done with this report as evidence."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-22T19:27:23.137Z"
sessionId: "se_fan0rytngv"
assignmentId: "as_l8lampk185"
costUsd: 1.0147938
tokens: 50740
turns: 25
createdAt: "2026-11-22T19:00:29.683Z"
updatedAt: "2026-11-22T19:27:23.137Z"
---
## What I did
I signed in as the test account dungeonrpg99-ops (us_u4mzpz4zc7) on live commit 167cf540. PR #555 is still open and not live. Both guards passed. ak_b0ijg20yed was open. `me` showed roles visitor+member and captains [gl_1ds3wl2n78]. I read the decision queue's routes as the test account and decided ak_b0ijg20yed with Confirm. Then I reset the account. I rewrote the topic page [dc_jix89oy4ve](../../wiki/2026-11/2026-11-06-test-github-account-dungeonrpg99-ops-x89oy4ve.md).

## Findings
- **Mine view (kr_lgft8zxocd).** I called `GET /api/buildings/town-hall/intray` with the test account's bearer at 18:59Z. It returns `defaultView: "mine"` and 13 routes. Only **ak_b0ijg20yed** (goal gl_1ds3wl2n78, owner dungeonrpg99-ops) has `mine: true, canDecide: true`. The other 12 have `mine: false, canDecide: false`, all on gl_town with owner Mitchell:
  - grants gr_93s00hyq1l, gr_3h504nqqdp, gr_6c24p5uy01, gr_mcuj10tupi, gr_k71b7b6px7, gr_xoso5f3oot
  - asks ak_9t2440s8l0, ak_yr1vgp15jz, ak_ls8kweomn7, ak_g31qpua2a3, ak_dhutjl05du, ak_uajugpkqri

  This evidence is API-only. Headless chromium reached only the muster.town collectives intro, not the queue panel.
- **Decision by a second human (kr_wrh4pcxhpk).** I sent `POST /api/asks/ak_b0ijg20yed/decide {"decision":"Confirm","note":"live check gr_0vuiuqcw8p step 2"}` and got 200.
  - The ask's history shows `decide by us_u4mzpz4zc7` at 2026-11-22T19:00:00.308Z.
  - Event 183435 `ask.decided` has by us_u4mzpz4zc7.
  - Thread entry **en_rdz91idr65** on jb_gr_0vuiuqcw8p (authorKind human) reads "dungeonrpg99-ops decided your ask … Confirm. live check gr_0vuiuqcw8p step 2". It names the test account, not Mitchell.
- **Reset.** At 19:00:0xZ, `POST /api/me/reset` returned rolesRemoved [role:member] and goalsReleased [gl_1ds3wl2n78]. Requests deleted or withdrawn: 0. Agents retired: none. At 19:00:07Z, `me` shows roles [role:visitor], canInteract false, accessRequest null, captains [], directGoals [], visitorAgents []. The account is free for other checks.
- **Small finding.** In the ask JSON, `decidedByName` is null. The decider's name shows only on the thread entry and the event.

## What I need from you
Close gr_0vuiuqcw8p with close_grant: all three of its key results now have live evidence.
