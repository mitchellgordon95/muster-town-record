---
id: "dc_8ue50ua1sq"
type: "report"
state: "building"
title: "Rollup 60: every report now threads into its job with \"what is left\"; the chain rule is built but its grant is held over ceiling with a red check (adjust by 150k or cut)"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_id4j1navsg","dc_hgsvgma4uo","dc_79i90mn89f","dc_gj3rgtzd6p","dc_6apgfql3r5"],"urls":[]}
tags: ["rollup","folded"]
verdict: "continue"
decision: "approve"
decisionNote: "Folded into the in-tray row of gr_2r17x8egrc: its ask shows there (1:1 mt_7b4zc7yja3)."
decidedBy: "system"
decidedAt: "2026-11-12T17:02:38.779Z"
sessionId: "se_an5a7c1p12"
createdAt: "2026-11-12T17:02:38.751Z"
updatedAt: "2026-11-12T17:02:38.779Z"
---
Live b9accd7 since 16:58 UTC today (PR #435, the jobs grant's step 2). Filed under the escalation rule: the chain-rule grant is held at its gate, over its ceiling, with its pull request's check red.

## Shipped

**1. Every session report now lands in its job's thread, with "what is left"**

**What it is:** Step 2 of the jobs grant you funded two hours ago. When a fork files a report, the town appends one entry to the grant's job in the same transaction: steps done, key results claimed, what is left, any top-up, any proposal. A grant step's report is refused without a "left" line. Budget holds are now keyed by the job's rule, not the lane, and the gate hold still works. Reports [dc_id4j1navsg](2026-11-12-submit-report-writes-the-entry-ruleblock-replaces-4j1navsg.md), [dc_hgsvgma4uo](2026-11-12-pr-435-merged-b9accd7a-parked-on-its-deploy-to-liv-svgma4uo.md), [dc_6apgfql3r5](2026-11-12-pr-435-is-live-b9accd7a-job-line-in-the-prompt-che-pgfql3r5.md); grant gr_9mp6v6vv8k.

**What you'd see:** GET /api/jobs/gr_9mp6v6vv8k shows rule ceiling, 12 entries, answers threaded under the reports they answer. A fork's prompt says "This session: job jb_gr_9mp6v6vv8k (rule ceiling, pocket gr_9mp6v6vv8k)". API-only change, no picture. Step 3 (the one answering loop) is on the queue.

**Your call:** None.

**2. The GitHub export survives commits made by hand on the repo**

**What it is:** Decision 5 of your 1:1 with the Secretary, verified live. Pix 1 initialised a repo with a README, made a hand commit, and ran the publish-check collective's export twice: both pushes merged over the foreign commits with no force push and no push error. Report [dc_79i90mn89f](2026-11-12-export-push-survives-foreign-commits-verified-live-i90mn89f.md).

**What you'd see:** The /publish-check/ repo on GitHub with the town's export commits on top of the README and the hand commit; the collective's publish line reads lastPushError null. No picture needed.

**Your call:** None.

**3. The chain rule is built, but its grant is held over ceiling with a red check**

**What it is:** Step 1 of the chain-rule grant: one building per chain of the goal tree, refused with 409 on create, attach, adopt and import, a human goal move allowed and recorded, and a boot audit event that should read 0 violations and 1 accepted exception (UI / UX under the Workshop, as you decided). It is on draft PR #436, whose CI check failed; the cause is not read yet. The grant has spent 241k of its 200k ceiling and is held. Report [dc_gj3rgtzd6p](2026-11-12-chain-rule-built-pr-436-open-parked-on-its-ci-3rgtzd6p.md); grant gr_2r17x8egrc.

**What you'd see:** PR #436 on GitHub with a red check. The gate row for the grant in your in-tray. Nothing live yet from step 1; step 2 (residents publish) has been live since 15:28 UTC.

**Your call:** Adjust the chain-rule grant by 150k to 350k so two small sessions fix the check, merge, read the boot audit and run the resident-publish demo, or cut it and leave PR #436 open with one key result unclaimed.

## Decided
- [dc_id4j1navsg](2026-11-12-submit-report-writes-the-entry-ruleblock-replaces-4j1navsg.md) → approve (PR #435 built, parked on CI)
- [dc_hgsvgma4uo](2026-11-12-pr-435-merged-b9accd7a-parked-on-its-deploy-to-liv-svgma4uo.md) → approve (PR #435 merged b9accd7a, parked on its deploy)
- [dc_79i90mn89f](2026-11-12-export-push-survives-foreign-commits-verified-live-i90mn89f.md) → approve (export verified live against foreign commits; decision 5 closed)
- [dc_gj3rgtzd6p](2026-11-12-chain-rule-built-pr-436-open-parked-on-its-ci-3rgtzd6p.md) → approve (chain rule built on draft PR #436; its merge assignment later cancelled and replaced by as_4rf8j6ss49 because the check failed)
- [dc_6apgfql3r5](2026-11-12-pr-435-is-live-b9accd7a-job-line-in-the-prompt-che-pgfql3r5.md) → approve (PR #435 live and checked; step 3 as_0rk272gsne pending)

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_mjr7nb438v Keep onboarding material within 24 h of main | kr_hee2pa2d5r onboarding lag under the 48 h line | on-track (daily sweep; today's 19:00 run waits on the retainer ask) | see the Town Hall gate |
| gr_9mp6v6vv8k Jobs, entries and one answering loop | kr_0neb2wqafu jobs readable by id | claimed ([dc_k90p1i7q74](2026-11-12-get-api-jobs-gr-9mp6v6vv8k-is-live-ceiling-job-one-0p1i7q74.md)) | about 215k / 1,350,000 |
| gr_9mp6v6vv8k | kr_xzdcf7d5i3 one loop, gate shows what is left | not-started (step 3 pending) | |
| gr_2r17x8egrc Chain rule and residents publish | kr_ig32y08ihi boot audit reads 0 violations, 1 exception | at-risk (PR #436 check red) | 241,354 / 200,000, held |
| gr_2r17x8egrc | kr_qswyvd1urh residents publish to their home building | on-track (Secretary's docs in the Town Hall cabinet; demo waits on ar_huzo0910nz) | |

Spend today by lane: exploration 0 tokens (free under the goal: 13,916,081), directed 299,192 tokens.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 0 proposals, 0 requests, 8 rollups ([dc_430cifl3v5](2026-11-06-rollup-50-grants-a-b-c-and-the-throwaway-closed-1-0cifl3v5.md), [dc_hf4ziawngu](2026-11-06-rollup-51-the-stranger-test-account-is-in-asked-to-4ziawngu.md), [dc_y3pqu4tfip](2026-11-07-rollup-52-onboarding-sweep-10-live-manual-fixed-th-pqu4tfip.md), [dc_4rb4ipqjz6](2026-11-10-rollup-55-from-first-visit-to-owning-a-goal-closed-b4ipqjz6.md), [dc_bwe6j2sf3r](2026-11-10-rollup-56-the-job-plan-is-filed-as-two-grants-to-f-e6j2sf3r.md), [dc_vddvmhc63k](2026-11-11-rollup-57-town-health-is-live-and-its-grant-closed-dvmhc63k.md), [dc_tw63frkzda](2026-11-12-rollup-58-chain-rule-stopped-on-ui-ux-under-the-wo-63frkzda.md), [dc_rdvub9l8u6](2026-11-12-rollup-59-the-root-town-s-record-is-on-github-publ-vub9l8u6.md))._
