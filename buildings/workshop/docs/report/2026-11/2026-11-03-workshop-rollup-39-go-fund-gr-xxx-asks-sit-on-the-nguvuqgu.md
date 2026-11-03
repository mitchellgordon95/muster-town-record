---
id: "dc_6fnguvuqgu"
type: "report"
state: "building"
title: "Workshop rollup 39: \"go fund gr_xxx\" asks sit on the grant's own in-tray row; checkpoint cards carry evidence and the real overspend (109%)"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_dz5v0ipflc","dc_q33fi73ahd","dc_bhgwa6993j","dc_6pt577j8b1","dc_txkusiipp8","dc_lq7t3ngg2a","dc_v6lehulzoc","dc_cvhofdr5xj","dc_ldga0zrpsv","dc_ex0zjdore7"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "pending"
sessionId: "se_3m4tdjupib"
createdAt: "2026-11-03T02:57:31.556Z"
updatedAt: "2026-11-03T02:57:31.556Z"
---
Live 85498fa (server restarted 02:47:12Z, read by Pix 1 at 02:47:27Z). Both items below are in it. Merged, waiting on the queued redeploy: PR #272 = 335c586 (ask lines render a table row as "a · b · c" instead of raw pipes). In CI: #259 (captain steering rights, main merged in as 9b40611), #273 (gr_yu6qw3j9x5 step 1), #274 (`read` on a topic page lists old revisions without their text). On a desk now: gr_8i952perny step 1 (Pix 4). The three grant-lane steps rollup 38 reported held "overdrafted" are all running or in CI.

## Shipped

**1. A rollup that only says "go fund gr_xxx" shows as a line on that grant's own in-tray row**
**What it is:** From our 1:1 mt_7b4zc7yja3. When a building's rollup asks you only for a decision on a grant (its proposal or checkpoint), it is no card of its own: its line about the grant sits on the grant's row, taken from the rollup's Needs section, or from the first other line naming the grant when Needs says nothing. A checkpoint row never lists its own report. PR #265 = 0f2271e and the two defects fixed in PR #270 = c106df1 (Pix 2: [dc_dz5v0ipflc](2026-11-02-265-ask-folding-live-checked-two-live-defects-fixe-5v0ipflc.md), live-checked [dc_q33fi73ahd](2026-11-02-270-live-checked-on-c106df1-no-self-ask-no-decided-3fi73ahd.md)). The last defect, raw `|` pipes when the line comes from a table row, is PR #272 = 335c586, merged and waiting on the redeploy ([dc_bhgwa6993j](2026-11-03-pr-272-merged-as-335c586-pipe-free-ask-lines-redep-gwa6993j.md); live check as_fztoul7292 parked on it).
**What you'd see:** Town Hall in-tray: gr_58n37j410s's checkpoint row carries one ask, from Onboarding's rollup [dc_u74lxukm10](../../../../bl_hzjw0z0zlz/docs/report/2026-11/2026-11-02-onboarding-rollup-2026-11-02-help-signs-done-membe-4lxukm10.md); gr_ukrou4zjha's row carries none (it used to list its own checkpoint report). The pipes in the picture go away once 335c586 is live.
![Onboarding's ask shown on gr_58n37j410s's checkpoint row in the Town Hall in-tray](/api/media/mf_gm7ckbq5vr.png)
**Your call:** None.

**2. A grant's checkpoint card says what shipped, and shows the real overspend**
**What it is:** The checkpoint row in the in-tray and its deck slide now carry the manager's evidence per key result (the checkpoint_grant notes: what shipped, where you check it) instead of only restating the key results and stop condition. PR #266 = 059b33f ([dc_6elfdumhqg](2026-11-02-checkpoint-card-shows-evidence-pr-266-open-waiting-lfdumhqg.md), live-checked [dc_6pt577j8b1](2026-11-02-266-checkpoint-card-live-checked-on-059b33f-row-un-t577j8b1.md)). That check found the row capping an overspent grant at "100%"; PR #271 = d2e55f7 removes the cap ([dc_txkusiipp8](2026-11-02-pr-271-merged-as-d2e55f7-checkpoint-row-shows-real-kusiipp8.md)), live-checked on 85498fa ([dc_lq7t3ngg2a](2026-11-03-271-live-checked-on-85498fa-gr-5ltmbf3a2f-s-in-tra-7t3ngg2a.md)): row and deck agree.
**What you'd see:** Town Hall in-tray, gr_5ltmbf3a2f's checkpoint row: "545k of 500k adj. tokens spent (109%)" above its evidence lines; the deck slide reads the same. The picture is from 059b33f, before the % fix: today the only difference is "109%" where it shows "100%".
![gr_5ltmbf3a2f's checkpoint row with per-key-result evidence](/api/media/mf_6p4a1xkqyv)
**Your call:** gr_5ltmbf3a2f (hosted collectives) is held at its checkpoint: Continue, Adjust or Cut it from that card.

## Decided
- [dc_dz5v0ipflc](2026-11-02-265-ask-folding-live-checked-two-live-defects-fixe-5v0ipflc.md) → approve (#265 live-checked; its two defects fixed in #270, merged).
- [dc_q33fi73ahd](2026-11-02-270-live-checked-on-c106df1-no-self-ask-no-decided-3fi73ahd.md) → approve (#270 live-checked, ask row pictured; pipes fix opened as #272).
- [dc_bhgwa6993j](2026-11-03-pr-272-merged-as-335c586-pipe-free-ask-lines-redep-gwa6993j.md) → approve (#272 merged as 335c586, redeploy queued, live check parked on it).
- [dc_6pt577j8b1](2026-11-02-266-checkpoint-card-live-checked-on-059b33f-row-un-t577j8b1.md) → approve (#266 live-checked; 100% cap defect sent to #271).
- [dc_txkusiipp8](2026-11-02-pr-271-merged-as-d2e55f7-checkpoint-row-shows-real-kusiipp8.md) → approve (#271 merged as d2e55f7).
- [dc_lq7t3ngg2a](2026-11-03-271-live-checked-on-85498fa-gr-5ltmbf3a2f-s-in-tra-7t3ngg2a.md) → approve (#271 live-checked on 85498fa: 109% on row and deck).
- [dc_v6lehulzoc](2026-11-03-gr-yu6qw3j9x5-step-1-caps-combine-as-the-minimum-e-lehulzoc.md) → approve (gr_yu6qw3j9x5 step 1: caps combine as the minimum on the path, explorer brief names §7-8; PR #273 in CI, continuation parked).
- [dc_cvhofdr5xj](2026-11-03-pr-259-needed-main-merged-in-main-moved-to-candire-hofdr5xj.md) → approve (PR #259 had main merged in as 9b40611, conflicts resolved toward main's canDirect; in CI, continuation parked; a backup.test.ts worker-thread timing test flakes under full-suite load, not the PR's).
- [dc_ldga0zrpsv](2026-11-03-rollup-materials-trimmed-to-items-18-19-archive-dc-ga0zrpsv.md) → approve (rollup materials page trimmed to items 18–19, archive [dc_0q9nlk7fa3](../../note/2026-11/2026-11-03-rollup-materials-archive-rollups-1-38-9nlk7fa3.md); `read` returned 367k chars of old revision text, fixed in PR #274, in CI).
- [dc_ex0zjdore7](2026-11-03-explore-under-gl-join-proposed-gr-eh6f1dl69n-since-0zjdore7.md) → approve (exploration: a returning captain has no "since you last reviewed" view; proposed gr_eh6f1dl69n, findings [dc_w97icr6obz](../../note/2026-11/2026-11-03-findings-a-returning-captain-has-no-since-you-last-7icr6obz.md); on its own in-tray row).

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_bwm0iz7rwl ask to captain a goal | kr_j1w17nw178 ask from the Goal tree, accept sets ownerId | not-started | 389,833 / 600,000 (as of rollup 38; no session since) |
| | kr_07d30db2bf core and server tests | not-started | |
| | kr_fd3ac479eb request shows in the in-tray and deck | not-started | |
| | kr_917dc5ba6d new owner steers live | not-started | |
| gr_zsm1piyqyx captain steering rights | kr_f1wzp12vtr captain decides a rollup (11-05) | on-track (PR #259, 9b40611 in CI; as_1s60qsde77 merges if green) | ≈241,900 / 500,000 (199,729 at rollup 38 + 42,139 this session) |
| | kr_k2gesp1b5e captain opens a 1:1 and plants a flag (11-05) | on-track (1:1 outside the subtree is 403 via main's canDirect; web step as_jr1thl80jr queued behind #259) | |
| | kr_xx9wtfnwh8 tests and docs/goals.md (11-04) | on-track (in #259) | |
| gr_yu6qw3j9x5 captained subtree throttled by desks and cap | kr_h0pqsgkov8 explorer brief names §7-8 (11-05) | on-track (PR #273 in CI; as_fycmamh1ch merges if green) | 54,927 / 500,000 |
| | kr_86wt7nnrfg caps combine as the minimum (11-06) | on-track (in #273) | |
| | kr_jya7n4g88a desksTotal on a captained goal (11-08) | not-started | |
| gr_8i952perny stop a funded grant | kr_ghexd88frr human-only stop (11-06) | on-track (step 1 running on Pix 4, as_nn00bsaeza: Grants.stop, wind-down, refund, KRs missed) | ≈103,100 so far / 500,000 (Bank booking at 02:50Z, session open) |
| | kr_4s0ccmvtsp wind-down first (11-07) | on-track (in step 1) | |
| | kr_kaz3nj127k money back (11-07) | on-track (in step 1) | |
| | kr_f46tddd9as KRs missed, in-tray row, manager told (11-08) | not-started | |
| gr_mjr7nb438v onboarding lag | kr_hee2pa2d5r onboarding material ≤ 24 h behind main for 7 days | on-track (sweep 6 on 11-02: lag 0 h, day 0 of 7; next sweep 19:00 UTC today, sc_nx8bwd5e5o) | not read this session / 600,000 |

Today's spend by lane: exploration 0 tokens (free under the goal: 0), directed 76,854 tokens.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 1 proposal (gr_eh6f1dl69n), 0 requests, 1 rollup ([dc_e5ymrwlhrv](2026-11-02-workshop-rollup-38-goal-editor-long-names-and-haik-ymrwlhrv.md))._
