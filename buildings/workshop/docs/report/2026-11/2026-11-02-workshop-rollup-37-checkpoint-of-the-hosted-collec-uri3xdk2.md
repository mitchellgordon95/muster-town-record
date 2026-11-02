---
id: "dc_zcuri3xdk2"
type: "report"
state: "building"
title: "Workshop rollup 37 (checkpoint of the hosted-collectives grant at 100%): goal tree editor, hosted collectives start with the founder's tree and a Workshop, Bank in Opus units; continue or cut"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_rlhn5rbixa","dc_kl0pnqpprj","dc_y3fn93mu4l","dc_w4ppnyouch","dc_4t7nyo7y02","dc_5h862nj7dr","dc_pm8nse129m","dc_t0bx9g9vvh","dc_1hm8dk92ba","dc_uu60h4svq6","dc_xg29dypbvz","dc_gwhoudbufd","dc_z7apbfzvie","dc_ct3vqo19hv","dc_s0ufgq62ux","dc_j5d74iyp8b"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-11-02T03:01:37.677Z"
sessionId: "se_qh9vv9dq7n"
assignmentId: "as_s3lflvalz2"
costUsd: 3.7699690499999994
tokens: 188498
turns: 49
createdAt: "2026-11-02T02:25:42.983Z"
updatedAt: "2026-11-02T03:01:37.677Z"
---
Live b2b8789 (health read 02:19 UTC today). This is also the 100% checkpoint of the hosted-collectives grant: its three key results are set below. Source for the Decided 1:1 line: meeting mt_a64faz59yr.

## Shipped

**1. The goal tree is an editor you can work in**
**What it is:** The Goal tree modal is a vertical canvas (root on top, children below, pan and zoom, click to select, keyboard walks the tree), each building shows − / + desk steps, a goal with no building gets a + that makes a lab there with one desk and a manager, the captain shows as a badge, the root always has a captain (you), and the split between tree and detail pane can be dragged, as your flag asked. PRs #237 = d9f28c5, #241 = af85f2a, #248 = 9c2d894, #249 = cf54c0c; all live-checked as a guest except the + (admin only).
**What you'd see:** Open the Goal tree: 20 boxes, your badge on the root; hover the line left of the detail pane and drag it; press + beside "no desks" on a goal without a building.
![Goal editor as a guest, detail pane widened to 761 px](/api/media/mf_ilj4o18rqn)
**Your call:** Try the + once on a goal with no building (it creates a real lab building).

**2. A hosted collective starts with the founder's tree and a Workshop**
**What it is:** A new hosted collective's goal tree is the founder's goal with them as captain (no Fund/Join/Trust pillars; Hollyville's empty ones retired), and a hosted World with only a Town Hall gets one lab "Workshop" with a manager-resident at a desk, on create and on reopen. A keyless admin's HUD reads "Add your API key to start". With a key, the explore tick reserving a chunk and the resident filing a grant proposal to the founder's in-tray on the founder's key is proven in a server test (PR #252, green, not merged: held by this checkpoint). PRs #243 = 6a541e4, #242 = 6e876b7.
**What you'd see:** muster.town/hollyville: Town Hall plus a Workshop with manager Dev on the map; /hollyville/api/goals root "Make money", captain Edward Li, no children.
![Hollyville as a guest: Town Hall and Workshop](/api/media/mf_24d26po5b6)
**Your call:** Start a throwaway collective from the homepage once, first without a key (you'd see the add-key line), then add a Console key (about $2–5): within about 10 minutes its in-tray should hold one grant proposal and its Bank one session on your key. That is the live check the grant's last key result needs.

**3. The Bank books in Opus 5.5 output tokens and keeps a 500,000-token operating reserve**
**What it is:** The accounting unit you chose in the 1:1 (Fable 2.5×, Haiku 0.025×; old figures untouched), and the reserve for 1:1s, meetings and directed work that funding may not dip into. PRs #231 = 7521c0b, #224 = 34de302; both live-checked. API and Bank page only, no picture.
**What you'd see:** Bank Overview: accounting model claude-opus-5-5, a reserve row of 500,000; a Fable session of 15,299 raw tokens books as 38,247.
**Your call:** None; the reserve blocks your own funding with a 409 when it would dip in. Set it to 0 to turn it off.

Also live since rollup 36, decided earlier (details on [dc_7lpbltjy1j](../../wiki/2026-10/2026-10-31-rollup-37-materials-pbltjy1j.md)): dismissed residents stay dismissed (#222), CPU post-mortem follow-ups (SQL aggregates e4c655e, events index #226, tick timing #229), symmetrical plain-tree map (#233), Planner revive on a Town Hall 1:1 (#236), Teo's desk setup recovery (#234), grant manager may set a key result under another building (#223).

## Decided
- [dc_rlhn5rbixa](2026-11-01-gr-5ltmbf3a2f-funded-plan-cut-into-three-steps-one-hn5rbixa.md) → approve (grant plan cut into three steps, one per key result).
- [dc_kl0pnqpprj](2026-11-01-hosted-goal-tree-is-the-founder-s-pr-243-open-wait-0pnqpprj.md), [dc_w4ppnyouch](2026-11-01-pr-243-hosted-goal-tree-is-the-founder-s-merged-as-ppnyouch.md) → approve (step 1 built, #243).
- [dc_y3fn93mu4l](2026-11-01-hosted-collectives-start-with-a-workshop-building-fn93mu4l.md), [dc_4t7nyo7y02](2026-11-01-pr-242-ci-failed-on-knip-two-unused-exports-fixed-7nyo7y02.md), [dc_5h862nj7dr](2026-11-01-pr-242-merged-main-conflict-at-docs-log-md-fixed-t-862nj7dr.md), [dc_pm8nse129m](2026-11-01-pr-242-hosted-collectives-start-with-a-workshop-me-8nse129m.md) → approve (step 2 built and merged, #242).
- [dc_t0bx9g9vvh](2026-11-01-hollyville-s-goal-tree-is-now-the-founder-s-243-6a-bx9g9vvh.md) → approve (step 1 live-checked as guest; kr_n2zh7s6s2s claimed).
- [dc_1hm8dk92ba](2026-11-01-hosted-collectives-step-2-live-checked-as-guest-ho-m8dk92ba.md) → approve (step 2 live-checked as guest; kr_god7otzibq claimed).
- [dc_uu60h4svq6](2026-11-01-hosted-step-3-traced-keyed-collective-s-first-tick-60h4svq6.md) → approve (step 3 traced in test, PR #252; its merge as_km3xgpu8j1 is held at this checkpoint).
- [dc_xg29dypbvz](2026-11-01-session-ended-without-a-report-retainers-live-set-29dypbvz.md), [dc_gwhoudbufd](2026-11-01-session-ended-without-a-report-write-the-checkpoin-houdbufd.md) → approve (died on the monthly spend limit at 21:23–21:31Z yesterday, before the requeue fix faf3eb3 was live; retried on your ask: the retainer one is queued as as_6w5ulpbb94, the checkpoint one is this report).
- [dc_z7apbfzvie](2026-11-01-session-ended-without-a-report-pr-248-ci-done-18a2-apbfzvie.md) → approve (overtaken: #248 merged as 9c2d894, live).
- [dc_ct3vqo19hv](2026-11-01-schedule-ended-daily-town-blockers-refresh-kr-hj8w-3vqo19hv.md) → approve (Town blockers schedule ended: its exploration lane no longer holds; dropped).
- [dc_s0ufgq62ux](2026-11-01-pr-249-goal-editor-divider-merged-as-cf54c0c-redep-ufgq62ux.md), [dc_j5d74iyp8b](2026-11-01-goal-editor-divider-249-cf54c0c-live-checked-as-a-d74iyp8b.md) → approve (divider drag #249 live-checked as guest).
- 1:1 today (mt_a64faz59yr): Try now on the Bank limit is not a wake bug (each clear released the held rows in 2–5 s; the first two batches died because Anthropic still said "monthly spend limit"). Real bug found: a rejected overage rate-limit event from my running 1:1 session recorded a plan-wide limit until 11-04 and held all new work for 2 minutes; PR #254 (Pix 1) ignores such a window while overage is allowed, merge pending its CI. New gap found today: retrying a grant's checkpoint assignment produced a copy held by the very checkpoint; PR #255 fixes it, merge queued on its CI.

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_5ltmbf3a2f hosted collectives (checkpoint) | kr_n2zh7s6s2s founder's tree, founder captain | claimed (guest live check, /hollyville/api/goals) | 545,488 / 500,000 |
| | kr_god7otzibq first Workshop + resident, add-key line | claimed (guest live check, /hollyville/api/town; the HUD line is in the bundle, admin-only, not seen on screen) | |
| | kr_f722z9ut50 keyed first exploration lands a proposal | on-track (server test in PR #252; no live run, Hollyville has no key) | |
| gr_mjr7nb438v onboarding lag (checkpoint, rollup 36) | kr_hee2pa2d5r material < 24 h behind | on-track | 445,387 / 300,000 |
| | kr_a9a473b0f8 catch-up sweep live | claimed | |
| | kr_df6a5cf736 daily sweep runs on its own | at-risk (held until its retainer is approved) | |
| | kr_c2989de971 lag measured and under 24 h | at-risk | |
| gr_bwm0iz7rwl ask to captain a goal (funded) | kr_j1w17nw178, kr_07d30db2bf, kr_fd3ac479eb, kr_917dc5ba6d | not-started (no session since funding) | 389,833 / 600,000 |

Today's spend by lane: exploration 0 tokens (free under the goal: 0), directed 106,216 tokens at the start of this session.

## Needs from Mitchell
1. Continue or cut the hosted-collectives grant at its checkpoint: continuing with about 100,000 more tokens merges #252, redeploys and runs the keyed live check in item 2 (which needs you or a test account to start the throwaway collective); cutting keeps key results 1 and 2 as claimed and leaves the keyed first exploration proven only in a test.
2. Nothing else.

_Already waiting in your in-tray: 1 proposal (gr_zsm1piyqyx), 0 requests, 0 rollups._
