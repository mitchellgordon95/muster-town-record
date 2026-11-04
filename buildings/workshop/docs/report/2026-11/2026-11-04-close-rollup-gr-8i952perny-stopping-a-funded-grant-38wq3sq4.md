---
id: "dc_cz38wq3sq4"
type: "report"
state: "building"
title: "Close rollup gr_8i952perny: stopping a funded grant works live end to end; grant closed as done (910,193 / 750,000, all four key results met, nothing to return)"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_z8mnleg08h","dc_6s0184hhvv","dc_ihgbot3mq8","dc_wdrq268xfl","dc_inj8i45d10","dc_3dpqecmor5","dc_gtgvqu4ni0","dc_4tev1v32ht","dc_c3h1ra5bgm","dc_08gl0xovmr"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/275","https://github.com/mitchellgordon95/muster-town/pull/280","https://github.com/mitchellgordon95/muster-town/pull/328"]}
tags: ["rollup","checkpoint"]
verdict: "stop"
decision: "pending"
sessionId: "se_sewtxh7306"
assignmentId: "as_agrj9j102y"
costUsd: 2.3579344000000004
tokens: 117897
turns: 18
createdAt: "2026-11-04T19:02:06.272Z"
updatedAt: "2026-11-04T19:02:06.272Z"
---
Live ad27e6f (health read 18:59:22Z). This is the close report for gr_8i952perny: its second 100% checkpoint came up, but the work was done, so I closed it as done instead of holding it (every further session was being charged to it).

## Shipped

**1. A human can stop a funded grant, and it was done for real**
**What it is:** Your stop of the throwaway grant gr_ikgaundf5p ("test stop", 32 minutes before this report) ran the whole wind-down: the stop is human-only, the grant went stopping then closed as stopped, its key result went missed with "Grant stopped: test stop", the close event recorded spent 144,584 / granted 5,000 / unspent 0 returned to the pool, the in-tray's stopped list carries it, and the manager was told. Code: PR #275 (227906a) and PR #280 (ae3c410), live since yesterday evening. Evidence: [dc_08gl0xovmr](2026-11-04-live-stop-evidence-for-gr-8i952perny-read-the-in-t-gl0xovmr.md), [dc_oghes5lgud](../../wiki/2026-10/2026-10-28-grants-key-results-and-the-town-hall-in-tray-hes5lgud.md).
**What you'd see:** Open gr_ikgaundf5p from the goal tree or in-tray: red "stopped" pill, "Mitchell stopped it: test stop", "0 unspent returned", the key result missed with your reason. The Bank page's free tokens match GET /api/bank.
![gr_ikgaundf5p stopped by Mitchell (live grant panel)](/api/media/mf_f7evv7o10g.png)
**Your call:** Two caveats on the "met" marks: the web in-tray's "Stopped: for the record" section only renders once PR #328 (the in-tray crash you flagged; CI green, merge and redeploy queued) is live, and a non-zero unspent return is exercised only by the core tests, since the test grant was already over budget. Flip kr_f46tddd9as or kr_kaz3nj127k to missed on the grant if either should stay open; otherwise none.

**2. The paperwork lesson**
**What it is:** The throwaway grant ran no work at all and was still charged 144,584 tokens by its kickoff and checkpoint sessions (two Fable sessions). gr_8i952perny itself overshot 750,000 by 160,193 the same way: checkpoint, live-check and close sessions after the work was finished.
**What you'd see:** GET /api/sessions?grantId=gr_ikgaundf5p: two sessions, 59,440 and 85,144 adjusted tokens, no PR. API-only; no picture.
**Your call:** None here. The fix is the bookkeeping-cost proposal already in your in-tray.

## Decided
- [dc_z8mnleg08h](2026-11-03-gr-8i952perny-step-1-grants-stop-in-draft-pr-275-c-mnleg08h.md), [dc_6s0184hhvv](2026-11-03-pr-275-merged-as-227906a-human-only-stop-of-a-fund-0184hhvv.md), [dc_ihgbot3mq8](2026-11-03-gr-8i952perny-step-2-stop-grant-in-the-web-in-tray-gbot3mq8.md), [dc_wdrq268xfl](2026-11-03-pr-280-conflicted-with-main-re-merged-at-323b62f-c-rq268xfl.md), [dc_inj8i45d10](2026-11-03-pr-280-merged-as-ae3c410-stop-grant-in-the-web-red-j8i45d10.md), [dc_gtgvqu4ni0](2026-11-03-picture-for-rollup-42-item-21-mf-iu22vr4eu2-stop-g-gvqu4ni0.md) → approve (the grant's build and live-check reports, PR #275 and PR #280; decided earlier).
- [dc_3dpqecmor5](2026-11-03-ae3c410-is-live-stop-grant-stopping-stopped-labels-pqecmor5.md) (Pix 2: ae3c410 live, Stop grant… button and stopped list on muster.town) → approve.
- [dc_4tev1v32ht](2026-11-03-workshop-rollup-42-checkpoint-stop-a-funded-grant-ev1v32ht.md) (first checkpoint, rollup 42) → continued by you at 750,000.
- [dc_c3h1ra5bgm](2026-11-04-gr-ikgaundf5p-still-proposed-at-12-00z-11-04-no-st-h1ra5bgm.md) (Pix 1: test grant not yet stopped at 12:00Z) → approve.
- [dc_08gl0xovmr](2026-11-04-live-stop-evidence-for-gr-8i952perny-read-the-in-t-gl0xovmr.md) (Pix 1: live evidence after your stop; found the in-tray crash, fix now in PR #328) → approve.

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_8i952perny (closed done) | kr_ghexd88frr human-only stop | met: tests green, live history "stop" by Mitchell | 910,193 / 750,000 |
| gr_8i952perny | kr_4s0ccmvtsp wind-down first | met: core test; live stopping → closed, no held rows | |
| gr_8i952perny | kr_kaz3nj127k money returned and shown | met: close event spent/granted/returned, Bank adds up; non-zero return core-tested only | |
| gr_8i952perny | kr_f46tddd9as KRs missed, in-tray, manager told | met: KR missed with reason, API stopped list, manager messaged; web row after PR #328 | |
| gr_bwm0iz7rwl Ask to captain | kr_j1w17nw178, kr_07d30db2bf, kr_fd3ac479eb, kr_917dc5ba6d | not started | 389,833 / 600,000 |
| gr_kdlogzzo5s Secretary | kr_spolcs3akx digest card first | on track: grouped card merged as d156a72, redeploy queued; first fire 07:00Z tomorrow | 910,950 / 1,500,000 |
| gr_kdlogzzo5s | kr_rl8l0xfrkm approved daily retainer | on track: retainer funded, schedule live | |
| gr_kdlogzzo5s | kr_nt0q4a3pmy 1:1 word becomes the decision | on track: verb and buttons live, no real 1:1 decision yet | |
| gr_kdlogzzo5s | kr_sdtzgbyrxn core and server tests | claimable: PR #300 and #303 green | |
| gr_30f8obzab8 Publish to GitHub | kr_gyqktjpevz Settings block | on track: API live (5baee1d), Settings block in review | 363,152 / 500,000 |
| gr_30f8obzab8 | kr_bm7q7rwxrk hourly push | on track: push code live, needs the repo and token from the outbox request | |
| gr_30f8obzab8 | kr_sqbsdpaju8 hosted collective's own repo | not started | |

Spend today by lane: exploration 72,681 tokens; directed 1,614,646 tokens.

## Needs from Mitchell
Nothing needed. The grant is closed; if you want the web "Stopped" row seen live before calling kr_f46tddd9as met, flip it to missed on the grant (only you can) and I reopen it under the next grant.

_Already waiting in your in-tray: 1 proposal (gr_cwwtrabt2o), 2 requests ([dc_31vt101dbe](../../../../../town-hall/outbox/2026-11/2026-11-04-start-a-throwaway-keyed-collective-to-check-gr-5lt-vt101dbe.md), [dc_wawcjkger2](../../../../../town-hall/outbox/2026-11/2026-11-04-publish-to-github-live-check-an-empty-github-repo-wcjkger2.md)), 0 rollups._
