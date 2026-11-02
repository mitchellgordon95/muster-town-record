---
id: "dc_rww8jufknn"
type: "report"
state: "building"
title: "Workshop rollup 12: Bank step 3 designed (24M grant → ~800K adjusted after conversion), blocked reasons part 2 live on 247f33a, Fly desk image push needs your flyctl token"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_tybdq79pr3","dc_y4w6dvrl5p","dc_9z9kqo7tyc","dc_1laow6beu4"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-26T22:05:38.985Z"
sessionId: "se_jol723j8no"
createdAt: "2026-10-26T21:31:12.070Z"
updatedAt: "2026-10-26T22:05:38.985Z"
---
## Shipped
- 247f33a LIVE (Keel, [dc_y4w6dvrl5p](2026-10-26-247f33a-is-live-api-blocked-and-the-grey-stack-bad-w6dvrl5p.md)): blocked reasons part 2. GET /api/blocked lists why each queued assignment can't start (4 agents right now: allowance spent, grant closed, deploy, colleague's assignment); the stack badge is grey; red dashed map lines to the blocker. The red "blocked N" badge, hover card and queue-row pill are on main but not yet seen in a browser (no idle blocked agent was in view).
- 882adb8 LIVE (me, [dc_9z9kqo7tyc](2026-10-26-gr-iq5m7dug56-checkpoint-filed-kr-vyrhhiyotb-on-tr-9kqo7tyc.md)): checkpoint_grant accepts a grant you already continued; verified by filing the gr_iq5m7dug56 checkpoint (kr_vyrhhiyotb on-track, rollup 11 linked).
- Nothing else merged this round. Bank step 3 (Lena, [dc_tybdq79pr3](2026-10-26-bank-step-3-design-done-no-code-yet-parked-so-the-bdq79pr3.md)) is designed, no code: stored tokens become adjusted, generated raw columns keep the sums, migration 036 converts once and writes an auditable bank.converted event. Live figures convert ÷30: 40M/day → ~1.33M/day, weekly cap 280M → ~9.33M, grant gr_iq5m7dug56 24M → 800K adjusted (spend re-derived from its sessions).

## Decided
- [dc_tybdq79pr3](2026-10-26-bank-step-3-design-done-no-code-yet-parked-so-the-bdq79pr3.md) (Lena, Bank step 3 design) → approve; resumes after the deploy and builds it.
- [dc_y4w6dvrl5p](2026-10-26-247f33a-is-live-api-blocked-and-the-grey-stack-bad-w6dvrl5p.md) (Keel, 247f33a live check) → continue → as_69zkwmncfz: finish the badge/hover/click/queue-row check with screenshots.
- [dc_9z9kqo7tyc](2026-10-26-gr-iq5m7dug56-checkpoint-filed-kr-vyrhhiyotb-on-tr-9kqo7tyc.md) (me, checkpoint filed) → approve.
- [dc_1laow6beu4](2026-10-26-wright-can-t-push-the-fly-desk-image-his-box-has-n-aow6beu4.md) (Root, Wright can't push the desk image) → approve; the push goes to you (below). New: Root as_wkx3ho7msn (exploration, held until the 10-27 allowance): make desk ensure recreate a Machine whose image is stale, keeping its volume, so future image pushes reach Fly desks without hand work.

## Key results
- kr_vyrhhiyotb (gr_iq5m7dug56): on-track. Spend 18,554,530 / 24,000,000 raw tokens (77%) at 21:48Z; Lena's step 3 session alone cost 2.31M. Steps 3, 4 (Keel) and 5 (Lena) are in flight; the 100% hold lands during step 4 or 5. Deaths: 14 in the 7 days to 10-26 21Z, 2 since funding; the zero-deaths clock starts after step 5.
- Exploration allowance 10-26: 14.6M of 10.4M; all exploration (Keel's check, Root's Fly fix, wake steps 1+2) is held until 00:00 UTC.

## Needs from Mitchell
1. Push the desk image and recreate the Fly desks (Wright's box has no flyctl, token or repo). From main: `FLY_ACCESS_TOKEN=<token> fly deploy --build-only --push --image-label desk -c fly.desk.toml`, then `fly machine destroy --force <id>` for each desk-* Machine in app muster-desks (keep the volumes; never `fly volumes destroy`). Until then Tae's, Keel's and Root's sessions post bare totals that the Bank back-fills (calibration 0.69 vs 1.02 real).
2. Still open from rollup 11: continue gr_iq5m7dug56 past the 100% hold, or adjust it to ~30M raw (≈1M adjusted once step 3's conversion lands) so step 5 fits.
