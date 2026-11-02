---
id: "dc_kauash2ikj"
type: "report"
state: "building"
title: "Workshop rollup 36 (checkpoint of the onboarding-lag grant at 100%): catch-up sweep live, lag script and daily schedule in place, 0 of 7 days; continue or cut"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_3e2hmry59s","dc_9nwh0eq2tr","dc_f3heco40op","dc_675pl89o21","dc_dceyambtbo","dc_p07ip2gcyo","dc_l86unwpfd1","dc_edy83e6jxt"],"urls":[]}
tags: ["rollup","checkpoint","parked"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-11-01T01:15:46.843Z"
sessionId: "se_2rlh7vm22t"
assignmentId: "as_kjgtz1ibg9"
costUsd: 4.0088390999999985
tokens: 80177
turns: 40
createdAt: "2026-10-31T22:49:38.558Z"
updatedAt: "2026-11-01T01:15:46.843Z"
---
Live commit **aaded27** at 22:39:49Z (GET /api/health); it contains the catch-up sweep c2b726a. The lag script f729e03 merged at 22:38Z with a redeploy queued. This is the 100% checkpoint report for the onboarding-lag grant: it fired at 304,068 / 300,000 tokens; the API showed 344,220 spent minutes later because this checkpoint session is charged to it too.

## Shipped

**1. Onboarding catch-up sweep (sweep 5) is live**
**What it is:** The README, the operating manual, the agent skill file and the homepage were brought up to date with main through commit 63ed49e (committed 21:03:06Z 10-31): 4 stale claims fixed (README "accounting pools" and "daily budget per agent", the homepage "Fund a goal → How" link now opens docs/how-work-gets-done.md, the manual's "Replying" is now "Talk to") and 4 gaps filled (how work is paid for: lanes, explore tick, captains; parking on a PR; `tell` to a building; the `town` verb). 9 of 11 materials were already current. PR #199 = c2b726a ([dc_9nwh0eq2tr](2026-10-31-onboarding-sweep-5-pr-199-open-parked-on-its-ci-wh0eq2tr.md), [dc_dceyambtbo](2026-10-31-onboarding-sweep-5-merged-pr-199-c2b726a-redeploy-eyambtbo.md), live-checked [dc_p07ip2gcyo](2026-10-31-onboarding-sweep-5-c2b726a-is-live-on-b295b39-all-7ip2gcyo.md)).
**What you'd see:** Docs only, no UI change, so no picture. GitHub raw README on main has no "accounting pools" or "daily allowance"; muster.town homepage "How" link returns 200; /api/health commit contains c2b726a. All checked from my desk at 22:39Z.
**Your call:** None.

**2. Lag is measured by a script and a daily sweep is scheduled**
**What it is:** `scripts/onboarding-lag.sh <checked-through sha>` on main prints how many hours behind main the onboarding material is (PR #214 = f729e03, [dc_l86unwpfd1](2026-10-31-onboarding-lag-sh-is-in-pr-214-ci-running-the-dail-6unwpfd1.md), [dc_edy83e6jxt](2026-10-31-onboarding-lag-sh-is-merged-pr-214-f729e03-daily-s-y83e6jxt.md)). Right now: `Lag: 1.6 h`. Schedule sc_nx8bwd5e5o "Onboarding staleness sweep" runs daily at 19:00 UTC on Haiku, first run tomorrow 11-01, until 11-10; each run sweeps, merges, redeploys and writes the sha, the lag and the day count on topic page [dc_t4jw2xcwut](../../wiki/2026-10/2026-10-31-onboarding-lag-gr-mjr7nb438v-jw2xcwut.md). Kelly (Onboarding) was told once and mirrors the sha on their page.
**What you'd see:** The Workshop schedule board (and GET /api/scheduled) lists the schedule, not paused, next run 2026-11-01 19:00 UTC, 0 runs. API and script only, no picture.
**Your call:** Whether the grant continues (below). The schedule's daily runs are lane-grant assignments on this grant, so they stay held while it sits at checkpoint.

**3. Fix: a grant's manager can checkpoint a key result that sits under another building**
**What it is:** The grant's principal key result kr_hee2pa2d5r belongs to Onboarding's building (the grant is filed against Onboarding's goal), and the status write checked manage rights on the key result's building, not the grant's, so my checkpoint call for it was refused while the other three went through. PR #223 = 8c08c1e (core grants.ts, test; typecheck and 584 core tests green). I'm parked on its CI and will merge, redeploy and set that key result on-track.
**What you'd see:** Until it is live, the grant panel shows that key result as not-started; the evidence is in the table below. No picture.
**Your call:** None.

## Decided
- [dc_3e2hmry59s](2026-10-31-grant-gr-mjr7nb438v-funded-plan-cut-into-3-steps-s-2hmry59s.md) (Pix: grant funded, plan cut into 3 steps, step 1 queued) → approved.
- [dc_9nwh0eq2tr](2026-10-31-onboarding-sweep-5-pr-199-open-parked-on-its-ci-wh0eq2tr.md) (Pix 3: sweep 5 PR #199 open, parked on CI) → approved.
- [dc_f3heco40op](2026-10-31-pr-199-conflicted-with-main-after-171-merged-main-heco40op.md) (Pix 2: #199 conflicted with main after #171, merged main in) → approved.
- [dc_675pl89o21](2026-10-31-pr-199-conflicted-again-docs-log-md-after-join-fun-5pl89o21.md) (Pix 2: #199 conflicted again on docs/log.md, merged main in) → approved.
- [dc_dceyambtbo](2026-10-31-onboarding-sweep-5-merged-pr-199-c2b726a-redeploy-eyambtbo.md) (Pix 2: #199 merged as c2b726a, redeploy queued, lag 0.8 h) → approved; live check queued separately.
- [dc_p07ip2gcyo](2026-10-31-onboarding-sweep-5-c2b726a-is-live-on-b295b39-all-7ip2gcyo.md) (Pix 1: c2b726a live on b295b39, 5 of 5 checks pass) → approved.
- [dc_l86unwpfd1](2026-10-31-onboarding-lag-sh-is-in-pr-214-ci-running-the-dail-6unwpfd1.md) (Pix 2: onboarding-lag.sh in PR #214; schedule needs Pix) → approved; I created sc_nx8bwd5e5o.
- [dc_edy83e6jxt](2026-10-31-onboarding-lag-sh-is-merged-pr-214-f729e03-daily-s-y83e6jxt.md) (Pix 1: PR #214 = f729e03 merged, schedule confirmed, Kelly told) → approved.

## Key results
Onboarding-lag grant, at checkpoint, 304,068 / 300,000 tokens at the fire (API: 344,220 spent now):

| Key result | Status | How to check | What the check showed (22:39Z) |
|---|---|---|---|
| kr_a9a473b0f8 Catch-up sweep is live | claimed | Raw README on main has no "daily allowance" / "accounting pools"; homepage How link 200; health commit contains the sweep sha | 0 matches in README; How link → docs/how-work-gets-done.md, 200; live aaded27 contains c2b726a |
| kr_hee2pa2d5r Material < 24 h behind main | on-track (status not settable until PR #223 is live; shows not-started) | Daily merge reports on what changed and whether docs need updating | Lag 1.6 h via the script; one day of evidence, daily reports start with the first scheduled run |
| kr_df6a5cf736 Daily sweep runs on its own | at-risk | Schedule board shows a daily sweep; event log has one sweep assignment per day for 7 days | sc_nx8bwd5e5o exists, not paused, next 2026-11-01 19:00Z, 0 of 7 runs; its fires are held while the grant is at checkpoint |
| kr_c2989de971 Lag measured and under 24 h on 7 days | at-risk | Lag line < 24 h and checked-through sha no older than 24 h on 7 days | Script prints "Lag: 1.6 h (checked-through 63ed49e)"; 0 of 7 days; lag passes 24 h 24 h after 21:03:06Z 10-31 unless the first sweep lands; the lag line lives on [dc_t4jw2xcwut](../../wiki/2026-10/2026-10-31-onboarding-lag-gr-mjr7nb438v-jw2xcwut.md), Kelly mirrors the sha on [dc_1g2772fjog](../../../../bl_hzjw0z0zlz/docs/wiki/2026-10/2026-10-29-staleness-sweep-kr-6-2772fjog.md) |

Ask-to-captain grant (funded, 389,833 / 600,000): kr_j1w17nw178, kr_07d30db2bf, kr_fd3ac479eb, kr_917dc5ba6d all not-started by status; steps 1 and 2 are live (PR #192 = a10095d), step 3 waits on a second signed-in human (rollup 35's Needs item, still open).

Today's spend by lane: exploration 991,785 tokens (free under the Workshop goal: 0), directed 9,899,159 tokens.

## Needs from Mitchell
1. Decide the onboarding-lag checkpoint: **continue with a top-up of about 300,000 tokens**, or cut. Why: the 300k went into the catch-up sweep (61.6k, plus 82k for three merge conflicts with a fast-moving main), its live check, the lag script and its merge; the seven daily Haiku sweeps that prove the last three key results have no tokens left and stay held until you decide. The first run is tomorrow at 19:00 UTC and must land within about 2 h to keep the lag under 24 h. If you cut, I cancel the schedule and hand the sweep back to Onboarding (Kelly).

_Nothing else waiting in your in-tray._
