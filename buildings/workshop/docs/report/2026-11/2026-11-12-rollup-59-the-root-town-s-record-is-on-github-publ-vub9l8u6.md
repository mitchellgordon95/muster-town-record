---
id: "dc_rdvub9l8u6"
type: "report"
state: "building"
title: "Rollup 59: the root town's record is on GitHub (Publish to GitHub grant closed as done, 380k back to the Bank); jobs are readable by id (step 1 of the jobs grant live, step 2 running)"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_rtxl283ru3","dc_k90p1i7q74","dc_blc4k6fcar","dc_3lkisf9v80","dc_6o92hunylm","dc_aq76a7tuv6","dc_miygymymkm","dc_ndrnfd7nkw","dc_2jdxiu72s1","dc_r7r08tuot9","dc_n7my2607r0"],"urls":["https://github.com/mitchellgordon95/muster-town-record","https://muster.town/api/jobs/gr_9mp6v6vv8k"]}
tags: ["rollup","grant-close"]
verdict: "continue"
decision: "pending"
sessionId: "se_lbk91t3bfp"
createdAt: "2026-11-12T16:05:57.818Z"
updatedAt: "2026-11-12T16:05:57.818Z"
---
Live 7c182fe since 16:02 UTC today (PR #432, jobs tables). Filed early, under the 4 h rule's escalation: a grant closed as done. The repo you set an hour and a half ago got its first push.

## Shipped

**1. The root town's record is on GitHub, and the Publish to GitHub grant is closed as done**
**What it is:** You set the root town's repo at 14:47 UTC. The hourly export pushed the whole town record there at 15:28 UTC: 3,246 files, no error, no drafts, no token. Pix 2 verified it from the API, the event log and a fresh clone. With that, all three key results of the grant had live evidence, so I closed it: 620,429 of 1,000,000 tokens spent, 379,571 returned to the Bank (gr_30f8obzab8, [dc_rtxl283ru3](2026-11-12-root-town-s-first-publish-to-github-push-verified-xl283ru3.md)).
**What you'd see:** https://github.com/mitchellgordon95/muster-town-record (public): README.md, town.json, buildings/ for all 8 buildings, library/, town-hall/, meetings/, events/, head commit d4e5e16. In the Town Hall → Settings → Publish to GitHub: "Last push 15:28 UTC · d4e5e16". No picture: the repo page is the view.
**Your call:** None. The three key results are marked met; flip one to missed on the grant only if the repo is not what you wanted.

**2. Any job is readable by id: GET /api/jobs/:id is live (step 1 of the jobs grant)**
**What it is:** The first step of the plan from your 1:1 on Monday: read-only jobs and entries tables, synced from the docs and events, and one route to read a job. A grant is a ceiling job with one entry per report and one per manager decision; a building is a building job; a schedule is a retainer job. Pix 2 checked it live (gr_9mp6v6vv8k, [dc_k90p1i7q74](2026-11-12-get-api-jobs-gr-9mp6v6vv8k-is-live-ceiling-job-one-0p1i7q74.md)). Step 2, submit_report writing the entry itself and budget rules replacing the lanes, queued itself and is running now.
**What you'd see:** API only, no UI yet: https://muster.town/api/jobs/gr_9mp6v6vv8k returns rule "ceiling", status open, 6 entries (propose, fund, two reports, two approves). https://muster.town/api/jobs/workshop returns the building job with 643 entries.
**Your call:** None.

## Decided
- [dc_rtxl283ru3](2026-11-12-root-town-s-first-publish-to-github-push-verified-xl283ru3.md) → approve (root push verified; grant closed)
- [dc_k90p1i7q74](2026-11-12-get-api-jobs-gr-9mp6v6vv8k-is-live-ceiling-job-one-0p1i7q74.md) → approve (GET /api/jobs live; step 2 self-queued)
- [dc_blc4k6fcar](2026-11-12-pr-432-merged-7c182fe7-parked-on-deploy-to-live-ch-c4k6fcar.md) → approve (PR #432 merged, parked on deploy)
- [dc_3lkisf9v80](2026-11-12-jobs-and-entries-read-only-pr-432-open-parked-on-c-kisf9v80.md) → approve (PR #432 open, parked on CI)
- [dc_6o92hunylm](2026-11-12-residents-publish-is-live-the-non-manager-publish-92hunylm.md) → approve (residents publish live; non-manager demo parked on the join request ar_huzo0910nz, resumes 18:30 UTC)
- [dc_aq76a7tuv6](2026-11-12-pr-427-merged-b6ac76b0-residents-publish-parked-on-76a7tuv6.md) → approve (PR #427 merged)
- [dc_miygymymkm](2026-11-12-residents-publish-pr-427-open-parked-on-ci-ygymymkm.md) → approve (PR #427 open)
- [dc_ndrnfd7nkw](2026-11-12-sweep-retainer-sc-nx8bwd5e5o-is-still-asked-80k-op-rnfd7nkw.md) → approve (onboarding retainer state read; nothing to re-ask)
- [dc_2jdxiu72s1](2026-11-12-web-for-every-manager-s-1-1-and-the-secretary-s-se-dxiu72s1.md) → approve (PR #426 web for 1:1s open)
- [dc_r7r08tuot9](2026-11-12-pr-426-merged-7be84c3c-web-for-every-manager-s-1-1-r08tuot9.md) → approve (PR #426 merged)
- [dc_n7my2607r0](2026-11-12-web-for-the-secretary-live-session-restarted-under-my2607r0.md) → approve (web for the Secretary live; WebFetch not yet seen, re-check queued 16:30 UTC)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_30f8obzab8 Publish to GitHub | kr_gyqktjpevz root repo set and pushed | met | 620,429 / 1,000,000 (closed) |
| gr_30f8obzab8 | kr_bm7q7rwxrk Settings block shows the push | met | |
| gr_30f8obzab8 | kr_sqbsdpaju8 hosted collective pushes | met | |
| gr_9mp6v6vv8k Jobs and entries | kr_0neb2wqafu GET /api/jobs/:id | claimed | 209,612 / 1,350,000 (step 2 running) |
| gr_9mp6v6vv8k | the other key results | not started | |
| gr_2r17x8egrc Chain rule and residents publish | kr_qswyvd1urh residents publish | claimed (Secretary evidence; non-manager demo pending) | under 200,000 (not re-read this session) |
| gr_2r17x8egrc | kr_ig32y08ihi chain rule, boot audit clean | at risk: waits on your UI / UX answer (rollup 58) | |
| gr_mjr7nb438v Onboarding within 24 h | kr_hee2pa2d5r lag under 48 h for 7 daily sweeps | day 3 of 7; today's 19:00 UTC run holds until the retainer is approved | sweeps draw on the retainer, not the grant / 800,000 |
Spend today by lane: exploration 0 tokens (free under the goal: 14,814,916), directed 257,398 tokens.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 0 proposals, 0 requests, 7 rollups ([dc_430cifl3v5](2026-11-06-rollup-50-grants-a-b-c-and-the-throwaway-closed-1-0cifl3v5.md), [dc_hf4ziawngu](2026-11-06-rollup-51-the-stranger-test-account-is-in-asked-to-4ziawngu.md), [dc_y3pqu4tfip](2026-11-07-rollup-52-onboarding-sweep-10-live-manual-fixed-th-pqu4tfip.md), [dc_4rb4ipqjz6](2026-11-10-rollup-55-from-first-visit-to-owning-a-goal-closed-b4ipqjz6.md), [dc_bwe6j2sf3r](2026-11-10-rollup-56-the-job-plan-is-filed-as-two-grants-to-f-e6j2sf3r.md), [dc_vddvmhc63k](2026-11-11-rollup-57-town-health-is-live-and-its-grant-closed-dvmhc63k.md), [dc_tw63frkzda](2026-11-12-rollup-58-chain-rule-stopped-on-ui-ux-under-the-wo-63frkzda.md))._
