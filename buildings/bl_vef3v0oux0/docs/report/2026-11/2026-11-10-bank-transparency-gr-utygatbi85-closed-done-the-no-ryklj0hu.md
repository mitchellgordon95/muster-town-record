---
id: "dc_3qryklj0hu"
type: "report"
state: "building"
title: "Bank Transparency: gr_utygatbi85 closed done, the non-grant half of Bank Spending now splits by lane"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_2dmufhdi7d","dc_k9d6d0zqk4","dc_p3dwrcuuvm","dc_lx4k06pbxn"],"urls":[]}
tags: ["rollup","grant-close"]
verdict: "stop"
decision: "pending"
sessionId: "se_nlc6drx77s"
createdAt: "2026-11-10T21:18:51.107Z"
updatedAt: "2026-11-10T21:18:51.107Z"
---
Live: 628dd939 since 21:14 UTC (PR #415, the one step of gr_utygatbi85).

## Shipped

**1. Bank Spending explains the half of spend that is not under a grant**

**What it is:** The grant you funded 50 minutes ago is done and closed: one step, one PR, 271,870 of 300,000 tokens spent, 28,130 returned to the Bank. Under each building's "Not under a grant" bucket the Bank now shows four lane rows: directed (asked for by a human), exploration, retainers and "before lanes" (work from before lanes existed). A check line confirms the four lanes add up to the bucket. Directed rows name who asked and link the meeting; exploration rows say which proposal the run became and whether you funded, rejected or withdrew it. Grant gr_utygatbi85; reports [dc_2dmufhdi7d](2026-11-10-non-grant-spend-by-lane-is-live-and-verified-both-mufhdi7d.md), [dc_k9d6d0zqk4](2026-11-10-pr-415-conflicted-with-main-merged-main-pushed-339-d6d0zqk4.md), [dc_p3dwrcuuvm](2026-11-10-pr-415-failed-ci-on-unused-exports-fixed-and-pushe-dwrcuuvm.md), [dc_lx4k06pbxn](2026-11-10-non-grant-spend-split-by-lane-pr-415-open-waiting-4k06pbxn.md).

**What you'd see:** Signed out, /workshop/?guest#/bank › Spending › Town Workshop › Not under a grant: directed 37.85M, before lanes 7.18M, exploration 3.56M, retainers 0.17M, summing to 48,756,218 adj. tokens with a ✓ line. The sidebar reads: "Of 74,284,490 adj. tokens not under a grant: 55,682,565 asked for by humans, 8,617,514 exploration (208 runs, 62 became proposals, 48 funded), 772,506 retainers, 9,211,905 from before lanes." `npm run check:finance` passes 49 of 49.

![Lane rows under Not under a grant](/api/media/mf_6240wtv3tn)

![Directed rows naming who asked](/api/media/mf_neg22gk1zf)

**Your call:** None. The grant is closed and both key results are marked met. One honest gap: 155 of 919 directed rows, 7.4M tokens, predate stored source ids and read "who asked is not recorded"; the data cannot fill it. If that falls short of the second key result, flip it to missed on the grant.

## Decided
- [dc_2dmufhdi7d](2026-11-10-non-grant-spend-by-lane-is-live-and-verified-both-mufhdi7d.md) → approve (step 1 done, live and verified signed out; grant closed with close_grant)
- [dc_k9d6d0zqk4](2026-11-10-pr-415-conflicted-with-main-merged-main-pushed-339-d6d0zqk4.md) → approve (PR #415 conflict with main resolved, parked on CI)
- [dc_p3dwrcuuvm](2026-11-10-pr-415-failed-ci-on-unused-exports-fixed-and-pushe-dwrcuuvm.md) → approve (PR #415 opened, parked on CI)
- [dc_lx4k06pbxn](2026-11-10-non-grant-spend-split-by-lane-pr-415-open-waiting-4k06pbxn.md) → approve (findings that sized the lane split)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_utygatbi85 | kr_k76nyweby5: Not under a grant splits by lane, lanes sum to the bucket | met (closed done) | 271,870 / 300,000 |
| gr_utygatbi85 | kr_v5419kedhk: directed rows name who asked, exploration rows name their proposal | met (closed done; 155 old rows say who asked is not recorded) | 271,870 / 300,000 |

Spend today by lane: exploration 51,316 tokens, directed 230 tokens. No funded grant left; nothing on the queue. Per your pause on exploration work (your 1:1 with the Secretary 50 minutes ago), I am queuing no exploration until you lift it.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 1 proposal (gr_3na7vdmd52), 0 requests, 0 rollups._
