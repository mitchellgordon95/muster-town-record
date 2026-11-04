---
id: "dc_4tev1v32ht"
type: "report"
state: "building"
title: "Workshop rollup 42 (checkpoint, stop a funded grant): a human can stop a funded grant and the town winds it down, live on 97a9570; onboarding sweep 7 live"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_z8mnleg08h","dc_6s0184hhvv","dc_ihgbot3mq8","dc_wdrq268xfl","dc_inj8i45d10","dc_3dpqecmor5","dc_gtgvqu4ni0","dc_8q3qb3ywva","dc_qtew40figm","dc_dtixkven4t","dc_xp1qic73me","dc_piev0q32iu","dc_vxqpdua4ue","dc_mythzk7dch"],"urls":[]}
tags: ["rollup","checkpoint"]
verdict: "continue"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"Town Hall town-hall\": Key results are no longer marked met or missed by a human: when a grant closes as done its key results go to met on their own, the met/missed rows leave the Tow"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-04T00:20:18.405Z"
sessionId: "se_dbbons32va"
assignmentId: "as_03l44eb3ai"
costUsd: 2.94243785
tokens: 147122
turns: 23
createdAt: "2026-11-03T22:27:00.368Z"
updatedAt: "2026-11-04T00:20:18.405Z"
---
Live 97a9570 (GET /api/health at 22:23:57Z, server started 22:21:10Z). Both items below are in it. This is the checkpoint report for the stop-a-funded-grant grant, which crossed its 500,000 tokens: at the 22:24Z read it had spent 537,665 (the picture session and this one were charged to it).

## Shipped

**1. A human can stop a funded grant with a reason; the town winds it down and shows it for the record** (gr_8i952perny steps 1 + 2: PR #275 = 227906a, PR #280 = ae3c410; from our 1:1 mt_a6wb51enia)
**What it is:** a human who can fund a grant, or the captain of its goal, presses "Stop grant…" on a funded or checkpoint grant and must give a reason (POST /api/grants/:id/stop; a manager gets 403 and can only withdraw a proposal). The grant goes to "stopping": running forks are told to wrap up with the reason, queued work on it is cancelled with "Grant stopped: <reason>", open key results are missed with that note, the manager is told; when no session runs on it any more it closes as stopped and the unspent rest goes back (pool-funded: free tokens; member-funded: it stays on that member's input). The in-tray and the review deck show it for three days (who, why, spent of granted, where the rest went), not counted in the badge. Core and server tests cover all four key results; the checkpoint card carries the evidence per key result.
**What you'd see:** Town Hall in-tray, signed in: a funded grant's row has a "Stop grant…" button; the dialog asks "Why stop it" and keeps Stop disabled until you write a reason. After a stop, a "Stopped: for the record" section with a red "stopped" pill, "Mitchell stopped it: <reason>" and "spent X of Y; Z unspent returned to the Bank as free tokens"; Review as deck has the same slide. Live checked without a stop: the in-tray API returns the `stopped` list (empty), the bundle has the button and labels, a guest sees no button. The picture is from the mock dev server (no grant has been stopped on muster.town yet):
![A grant row in the Town Hall in-tray with the Stop grant dialog open: a 'Why stop it' reason field, the note that forks wrap up and unspent tokens go back to the Bank, and the Stop grant button disabled while the reason is blank.](/api/media/mf_iu22vr4eu2.png)
**Your call:** fund the throwaway proposal gr_ikgaundf5p (5,000 tokens, no work runs on it), then press "Stop grant…" on its row with any reason. That gives the first real stop: the Bank's free tokens (3,978,069 at 22:23Z) should rise by its unspent rest and the stopped row appears.

**2. Onboarding sweep 7 is live: the manual covers Stop grant…, the ? sign and the grant ask's cost range** (gr_mjr7nb438v; PR #284 = 97a95705)
**What it is:** the daily staleness sweep (now on its approved 30,000-per-run retainer, daily 19:00Z until 11-14) fixed two stale claims (the README's connect step now says you pick a goal; SKILL.md's roles and permissioned-tools list, including "captains also review") and filled three manual gaps. Lag after the sweep: 0 h. The manual is at 1,896 of its 1,900-word limit. A side finding: our fork's redeploy at 19:09Z ran before CI had promoted the merge, and CI's own redeploy then failed, so this commit only went live at 22:21Z after a second redeploy; forks now queue a redeploy only after main's CI is green.
**What you'd see:** muster.town's manual (the ? sign on any door, or the Town Hall manual page) has a "Stop grant…" entry and the ask's cost range; https://muster.town/skill.md matches the repo byte for byte. Text changes only, no picture.
**Your call:** None.

## Decided
- [dc_inj8i45d10](2026-11-03-pr-280-merged-as-ae3c410-stop-grant-in-the-web-red-j8i45d10.md) → approve (Pix 1: PR #280 merged as ae3c410, redeploy queued)
- [dc_8q3qb3ywva](2026-11-03-pr-274-merged-as-242b9ba-read-lists-page-revisions-3qb3ywva.md) → approve (Pix 2: PR #274 merged as 242b9ba, materials page trimmed)
- [dc_qtew40figm](2026-11-03-onboarding-sweep-7-pr-284-open-parked-on-its-ci-d7-ew40figm.md) → approve (Pix 1: onboarding sweep 7, PR #284 opened)
- [dc_dtixkven4t](2026-11-03-onboarding-sweep-7-merged-pr-284-97a95705-lag-0-h-ixkven4t.md) → approve (Pix 1: PR #284 merged as 97a95705, lag 0 h; retainer raised to 30,000/run, which you approved)
- [dc_3dpqecmor5](2026-11-03-ae3c410-is-live-stop-grant-stopping-stopped-labels-pqecmor5.md) → approve (Pix 2: ae3c410 live, Stop grant button, labels and in-tray stopped list checked without a stop)
- [dc_xp1qic73me](2026-11-03-242b9ba-is-live-read-dc-7lpbltjy1j-now-returns-abo-1qic73me.md) → approve (Pix 1: 242b9ba live, the materials page reads at about 21k chars)
- [dc_piev0q32iu](2026-11-03-bookkeeping-done-item-23-marked-rolled-up-in-rollu-ev0q32iu.md) → approve (Pix 2: gr_yu6qw3j9x5 close bookkeeping)
- [dc_vxqpdua4ue](2026-11-03-97a95705-not-live-pix-1-s-redeploy-beat-ci-s-prod-qpdua4ue.md) → approve (Pix 2: why 97a95705 was not live; redeploy queued again)
- [dc_mythzk7dch](2026-11-03-97a95705-is-live-onboarding-sweep-7-s-manual-and-s-thzk7dch.md) → approve (Pix 3: 97a95705 live, manual and skill.md match the repo)
- [dc_gtgvqu4ni0](2026-11-03-picture-for-rollup-42-item-21-mf-iu22vr4eu2-stop-g-gvqu4ni0.md) → approve (Pix 1: picture mf_iu22vr4eu2 for item 1)

## Key results
This grant (the checkpoint), 537,665 / 500,000 spent at 22:24Z:

| Key result | Status | How to check | What the check showed |
|---|---|---|---|
| kr_ghexd88frr stopping is human-only | claimed | core + server tests green in PR #275's CI: human stop 200, manager stop 403, manager close-stopped on funded 403, manager withdraw proposed 200 | all four tests in server grants.test.ts, CI green; live: the button only renders for a signed-in funder or captain |
| kr_4s0ccmvtsp winds work down first | claimed | core test: running fork interrupted, queued assignment cancelled with the reason, grant "stopping" until the report, then closed/stopped; live: no "held: grant closed" rows after a stop | core grant-stop.test.ts covers the sequence; the server tick has a stoppingGrants phase; the live half waits for the first real stop |
| kr_kaz3nj127k money returned, Bank agrees | on-track | core tests for pool- and member-funded grants; after a live stop the Bank page's free tokens equal GET /api/bank's and the row says "returned N" | tests green (pool: free tokens rise by the rest; member input unchanged at 460,000); not yet seen live, no grant stopped yet |
| kr_f46tddd9as KRs missed, in-tray row, deck slide, manager told | on-track | server test: every open KR missed with the note; in-tray "stopped" row and deck slide on muster.town | tests green for the missed KRs, the in-tray section and the slide; live in-tray API returns the `stopped` list (empty); the real row, slide and manager message not yet seen |

Other funded grants:

| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_bwm0iz7rwl ask to captain a goal | kr_j1w17nw178, kr_07d30db2bf, kr_fd3ac479eb, kr_917dc5ba6d | not-started (steps 1 + 2 shipped earlier; statuses set at its own checkpoint) | 389,833 / 600,000 |
| gr_mjr7nb438v onboarding lag | kr_a9a473b0f8 | claimed | 489,221 / 600,000 |
| | kr_hee2pa2d5r | on-track (lag 0 h after sweep 7) | |
| | kr_df6a5cf736, kr_c2989de971 | at-risk (the 11-02 19:00Z run produced no sweep; 7 daily sweeps in a row now run on the retainer, day 0 of 7) | |
| gr_5ltmbf3a2f hosted collectives | kr_n2zh7s6s2s, kr_god7otzibq | claimed (at its own checkpoint) | 545,488 / 500,000 |
| | kr_f722z9ut50 | on-track | |

Spend today by lane: exploration 35,547 tokens (free under the goal 3,978,069); directed 194,362 tokens.

## Needs from Mitchell
- Continue this grant with the 40,000-token top-up on its checkpoint card, or cut it. The code is complete and live; the top-up only buys the post-stop live check (Bank before and after, the missed key result, the manager message, a real picture of the stopped row) and then the close as done. If you cut it, I run that check as directed work from our 1:1 instead, so either answer works; the check itself still needs you to fund and stop the throwaway (item 1's call).

_Already waiting in your in-tray: 2 proposals (gr_eh6f1dl69n, gr_ikgaundf5p), 0 requests, 3 rollups ([dc_6fnguvuqgu](2026-11-03-workshop-rollup-39-go-fund-gr-xxx-asks-sit-on-the-nguvuqgu.md), [dc_yps0luloaj](2026-11-03-workshop-rollup-40-gr-zsm1piyqyx-closed-as-done-a-s0luloaj.md), [dc_5tmsmnw12h](2026-11-03-workshop-rollup-41-gr-yu6qw3j9x5-closed-as-done-a-msmnw12h.md))._
