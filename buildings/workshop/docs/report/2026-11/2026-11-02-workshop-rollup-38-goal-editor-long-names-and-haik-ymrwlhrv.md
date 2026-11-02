---
id: "dc_e5ymrwlhrv"
type: "report"
state: "building"
title: "Workshop rollup 38: goal editor long names and Haiku-named labs, withdraw_grant, Bank overage and retry fixes, sweep 6; the Bank is overdrafted and holds three funded-grant steps"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_pzxzjvtq22","dc_2p5ax6ol4v","dc_0tqkhl4enf","dc_txmegbsqqi","dc_k9vh60jxni","dc_oqg127jyf4","dc_6jx7gb60lw","dc_7wtp3r82kd","dc_vkp2eipsec","dc_b277emmn6i","dc_arbyy3hid2","dc_my4hqfrikz","dc_862vuglvps","dc_z4jli0m3fq","dc_motiu8tr6k","dc_iu1swoejal","dc_6elfdumhqg","dc_pom9x1vjur","dc_9tmcw7ly77","dc_loqehjmgjd"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "pending"
sessionId: "se_97jgbfuzmd"
createdAt: "2026-11-02T18:05:58.154Z"
updatedAt: "2026-11-02T18:05:58.154Z"
---
Live 92336d0 (health read by Pix 2 at 18:02:35Z, server started 18:02:14Z). Everything below is in it. Not yet live: the ask-folding in-tray rows (#265, merged, waiting on the next redeploy) and the checkpoint card with evidence (#266, merging now); both come in rollup 39 with a picture.

## Shipped

**1. Goal editor: long building names fit, and a lab you add from the canvas gets a short Haiku name**
**What it is:** Your flag [dc_42c9cjbzls](../../flag/2026-11/2026-11-01-the-desk-add-and-remove-on-goal-nodes-in-the-goal-c9cjbzls.md). A building row in a goal box cuts a long name with an ellipsis (hover shows it whole) so the − / + desk steps stay in place; pressing + on a goal with no building now names the new lab with one cheap-model call (booked as a `naming` session on its manager; falls back to the goal's short text). PR #256 = c322b25, guest-checked by Pix 1 ([dc_k9vh60jxni](2026-11-02-pr-256-c322b25-live-long-building-names-fit-on-the-vh60jxni.md)).
**What you'd see:** Goal tree, the "People who would use Muster Town know…" box: name cut at 100% and at Fit, "· 1" and − / + inside the box.
![Goal editor: long building name cut with an ellipsis, desk steps in place](/api/media/mf_q18ln94ob8)
**Your call:** Press + once on a throwaway goal with no building: the toast should carry a short place name, and the Bank a `naming` session. That is the only part not run live (agents can't create buildings).

**2. A manager can withdraw their own grant proposal**
**What it is:** New tool withdraw_grant (from our 1:1 mt_a6wb51enia): a manager or a funder pulls a proposed or countered grant with a required note; it leaves your in-tray and the deck, its key results archive, the note stays in the grant's History and reaches every funder's inbox. A funded grant is refused with "Close it with close_grant when its work is done, or ask a human to cut it." PR #264 = 0d0da02 (Pix 1 [dc_0tqkhl4enf](2026-11-02-withdraw-grant-tool-merged-pr-264-0d0da02-redeploy-qkhl4enf.md); live-checked by Pix 2 [dc_2p5ax6ol4v](2026-11-02-withdraw-grant-is-live-92336d0-0d0da02-funded-refu-5ax6ol4v.md): verb listed, funded refusal confirmed). API and tool only, no picture.
**What you'd see:** Nothing until a proposal is withdrawn: then no row for it in the in-tray and a "withdrawn" line in its History.
**Your call:** None.

**3. Bank limit fixes and the Haiku onboarding sweep**
**What it is:** (a) A rejected overage rate-limit event no longer records a plan-wide limit that holds all new work (the cause of the "Try now" that woke nobody), PR #254 = dab5b9b ([dc_7wtp3r82kd](2026-11-02-pr-254-live-checked-server-and-desk-image-both-on-tp3r82kd.md)). (b) Retrying a checkpoint assignment keeps its system author, so the copy isn't held by the very checkpoint, PR #255 = e992393 ([dc_arbyy3hid2](2026-11-02-pr-255-live-in-ba6cd93-a-checkpoint-retry-keeps-it-byy3hid2.md)). (c) With the sweep retainer you approved (45,000 tokens, 5,000 per run), onboarding sweep 6 ran on Haiku: PR #258 = d75b388, lag 0 h, day 0 of 7 ([dc_my4hqfrikz](2026-11-02-onboarding-sweep-6-merged-pr-258-d75b388-redeploy-4hqfrikz.md)). API-only, no picture.
**What you'd see:** Bank Overview: no "limit until 11-04" line; Town Workshop schedule board: the sweep's next run tonight 19:00 UTC.
**Your call:** None.

## Decided
- [dc_pzxzjvtq22](2026-11-02-pr-265-merged-0f2271e-redeploy-queued-parked-to-li-xzjvtq22.md) → approve (#265 merged as 0f2271e; its live check waits on the deploy).
- [dc_2p5ax6ol4v](2026-11-02-withdraw-grant-is-live-92336d0-0d0da02-funded-refu-5ax6ol4v.md) → approve (withdraw_grant live-checked).
- [dc_0tqkhl4enf](2026-11-02-withdraw-grant-tool-merged-pr-264-0d0da02-redeploy-qkhl4enf.md), [dc_txmegbsqqi](2026-11-02-withdraw-grant-not-live-yet-live-024b236-predates-megbsqqi.md) → approve (withdraw_grant built and merged; first live check found it not yet deployed).
- [dc_k9vh60jxni](2026-11-02-pr-256-c322b25-live-long-building-names-fit-on-the-vh60jxni.md), [dc_oqg127jyf4](2026-11-02-pr-256-merged-as-c322b25-redeploy-queued-parked-fo-g127jyf4.md) → approve (flag [dc_42c9cjbzls](../../flag/2026-11/2026-11-01-the-desk-add-and-remove-on-goal-nodes-in-the-goal-c9cjbzls.md): #256 merged and guest-checked).
- [dc_6jx7gb60lw](2026-11-02-pr-254-merged-as-dab5b9b-redeploy-with-desk-image-x7gb60lw.md), [dc_7wtp3r82kd](2026-11-02-pr-254-live-checked-server-and-desk-image-both-on-tp3r82kd.md), [dc_vkp2eipsec](2026-11-02-try-now-did-wake-the-held-work-real-bug-an-overage-p2eipsec.md) → approve ("Try now" measured as not a wake bug; the overage window fix #254 merged and live-checked).
- [dc_b277emmn6i](2026-11-02-pr-255-merged-as-e992393-redeploy-queued-77emmn6i.md), [dc_arbyy3hid2](2026-11-02-pr-255-live-in-ba6cd93-a-checkpoint-retry-keeps-it-byy3hid2.md) → approve (checkpoint retry fix #255 merged and live-checked).
- [dc_my4hqfrikz](2026-11-02-onboarding-sweep-6-merged-pr-258-d75b388-redeploy-4hqfrikz.md) → approve (sweep 6 merged, lag 0 h).
- [dc_862vuglvps](2026-11-02-grant-gr-mjr7nb438v-adjusted-600-000-tokens-2vuglvps.md) → approve (onboarding-lag grant continued at 600,000; page updated).
- [dc_z4jli0m3fq](2026-11-02-captain-steering-gates-in-pr-259-core-server-waiti-jli0m3fq.md) → approve (captain rights step 1 built as PR #259; its merge is now held, see Needs).
- [dc_motiu8tr6k](2026-11-02-fold-go-fund-gr-xxx-rollups-into-the-grant-s-in-tr-tiu8tr6k.md), [dc_iu1swoejal](2026-11-02-pr-265-was-conflicting-with-main-merged-main-in-bf-1swoejal.md) → approve (#265 built, main merged in, CI green, merged today).
- [dc_6elfdumhqg](2026-11-02-checkpoint-card-shows-evidence-pr-266-open-waiting-lfdumhqg.md) → approve (#266 checkpoint evidence card built; merging now).
- [dc_pom9x1vjur](2026-11-02-gr-kph1zjjrzg-rejected-acknowledged-nothing-re-pro-m9x1vjur.md) → approve (gr_kph1zjjrzg rejection acknowledged).
- [dc_9tmcw7ly77](2026-11-02-filed-gr-yu6qw3j9x5-captain-subtree-throttled-by-d-mcw7ly77.md), [dc_loqehjmgjd](2026-11-02-proposed-gr-8i952perny-stop-a-funded-grant-human-o-qehjmgjd.md) → approve (the two grants you funded at 03:2xZ; their first steps are queued and held, see Needs).

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_bwm0iz7rwl ask to captain a goal | kr_j1w17nw178 ask from the Goal tree, accept sets ownerId | not-started | 389,833 / 600,000 |
| | kr_07d30db2bf core and server tests | not-started | |
| | kr_fd3ac479eb request shows in the in-tray and deck | not-started | |
| | kr_917dc5ba6d new owner steers live | not-started | |
| gr_zsm1piyqyx captain steering rights | kr_f1wzp12vtr captain decides a rollup (due 11-05) | not-started (PR #259 built, green; its merge held: overdrafted) | 199,729 / 500,000 |
| | kr_k2gesp1b5e captain opens a 1:1 and plants a flag (11-05) | not-started (web step queued behind #259) | |
| | kr_xx9wtfnwh8 tests and docs/goals.md (11-04) | not-started (in #259) | |
| gr_yu6qw3j9x5 captained subtree throttled by desks and cap | kr_h0pqsgkov8 explorer brief names §7-8 (11-05) | not-started (step 1 held: overdrafted) | 0 / 500,000 |
| | kr_86wt7nnrfg caps combine as the minimum (11-06) | not-started (step 1 held) | |
| | kr_jya7n4g88a desksTotal on a captained goal (11-08) | not-started | |
| gr_8i952perny stop a funded grant | kr_ghexd88frr human-only stop (11-06) | not-started (step 1 held: overdrafted) | 0 / 500,000 |
| | kr_4s0ccmvtsp wind-down first (11-07) | not-started (step 1 held) | |
| | kr_kaz3nj127k money back (11-07) | not-started (step 1 held) | |
| | kr_f46tddd9as KRs missed, in-tray row, manager told (11-08) | not-started | |

Today's spend by lane: exploration 41,899 tokens (free under the goal: 0), directed 1,477,060 tokens.

## Needs from Mitchell
1. The Bank is overdrafted: its usable balance (balance less unavailable credit less the 500,000 reserve) no longer covers the funded grants' remaining tokens, so the town holds three grant-lane steps "overdrafted": the merge of PR #259 (captain steering rights, gr_zsm1piyqyx), step 1 of gr_yu6qw3j9x5 and step 1 of gr_8i952perny. Directed work still runs (1.48 M tokens today). Either add input to the Bank, lower the reserve, or cut one of the two grants funded at 03:2xZ; the Bank page's Free tokens table lists each held claim and how far short it is.
2. Nothing else.

_Nothing else waiting in your in-tray._
