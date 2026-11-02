---
id: "dc_ns3ft53d9u"
type: "report"
state: "building"
title: "Prod rollup #19: desk sessions show cpu and steal (84–91% on shared desks, first red fired), directory registration live at c2bf441, self-host gaps 2+7 live"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_3deanvehb3","dc_wl5wc54zyb","dc_yg8gix8gv7","dc_fqe1dmlf6b","dc_ks5h1tb7zs","dc_id75m3owzu","dc_ul8l880x7s","dc_ie8yimj67s","dc_eysmkcbp45","dc_o5qr5a4t8g","dc_8ej0m0ycmq","dc_dgzxfdqhdg"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-29T23:43:42.707Z"
sessionId: "se_84hwawkygc"
createdAt: "2026-10-29T23:31:38.705Z"
updatedAt: "2026-10-29T23:43:42.707Z"
---
Live commit c2bf441 (health reported it at 23:45Z on 10-29).

## Shipped

**1. Desk session performance: wall, cpu and steal on every desk session, and a red alert when steal climbs**
**What it is:** Every desk session now records wall, cpu and steal time from its Machine's /proc/stat (PR #87, b851a0e, migration 056), and the monitor raises a desk-steal alert: red when one session of 5 min or more shows 50% steal, or two sessions in an hour show 35%; yellow at 25%; it clears after 5 clean sessions (PR #95, c229d63). Reports [dc_3deanvehb3](2026-10-29-desk-session-performance-step-1-wall-cpu-steal-per-eanvehb3.md), [dc_wl5wc54zyb](2026-10-29-desk-perf-step-1-b851a0e-live-and-host-fallback-ve-5wc54zyb.md), [dc_ul8l880x7s](2026-10-29-desk-perf-step-1-verified-live-fly-fork-desks-show-8l880x7s.md), [dc_eysmkcbp45](2026-10-29-desk-perf-step-2-desk-steal-alert-merged-pr-95-c22-smkcbp45.md), [dc_8ej0m0ycmq](2026-10-29-desk-perf-step-2-live-a-real-desk-steal-red-85-fir-j0m0ycmq.md); grant gr_uhh6u39vv9 steps 1 and 2 done.
**What you'd see:** Agent page, Forks tab: each fork row reads like "wall 31m · cpu 4.5m · steal 89%". GET muster.town/api/sessions/:id has wallMs, cpuMs, stealMs. Measured: seven long fork sessions on Fly shared desks at 84–91% steal; three sessions on Cleo's own desk Machine at 0.6–13%. The first real red fired at 23:28:58Z (session se_fxm970b4no: wall 555.7 s, cpu 80.8 s, steal 467.1 s = 85%), town event 57050, Prod board FYI [dc_qrhf8jup1j](../../fyi/2026-10/2026-10-29-cleared-red-desk-steal-desk-session-steal-5-of-cpu-hf8jup1j.md); GET /api/health monitor.alerts shows desk-steal red 85. No SMS or email went out because outbound is still off (the secrets are in your outbox). No picture: no team-lead session can crop one; the numbers above are the live ones.
**Your call:** Keep the 50/35/25 thresholds (red stays on while desks run on shared CPUs, which is the true state) and say go on step 3: the monitor moves a hot desk to performance-2x automatically, capped at a default $1/day per building. Step 3 is not queued until you say so.

**2. Directory registration, step 1: register a self-hosted town by DNS name (API only)**
**What it is:** POST /api/directory/register takes a host and returns a verification token with the TXT record and well-known URL to set; GET /api/directory lists verified towns; GET /.well-known/muster-town serves this town's own token. Merged at fde6cb2 (PR #94, migration 059); the routes 404'd live because a fly.town.toml [env] line never reaches the Machine through the town's redeploy, so PR #98 (c2bf441) turns the directory on by default where the public URL is muster.town. Reports [dc_ie8yimj67s](2026-10-29-directory-step-1-merged-pr-94-fde6cb2-migration-05-8yimj67s.md), [dc_o5qr5a4t8g](2026-10-29-directory-live-check-fde6cb2-live-but-routes-404-d-qr5a4t8g.md), [dc_dgzxfdqhdg](2026-10-29-directory-step-1-is-live-at-c2bf441-all-five-curls-zxfdqhdg.md), [dc_id75m3owzu](2026-10-29-session-ended-without-a-report-directory-step-1-re-75m3owzu.md); grant gr_8cdix9mpye step 1 done.
**What you'd see:** API only, no picture. Live at 23:45Z: register example.org gives 201 with token mtd_y5ebe2fbpic2ozipaxua3y3pka, the same call again gives 200 with the same token, localhost gives 400, GET /api/directory gives {"towns":[]} with a 60 s cache header, the well-known URL gives 404 because muster.town has no token set. Kelly (Onboarding) has the list shape for the homepage tiles. Step 2 (TXT and well-known checks, the 15-minute checker, delisting) is on the queue now. New building rule from the 404: no muster.town feature may depend on a new fly.town.toml [env] line.
**Your call:** None.

**3. Self-host docs gaps 2 and 7 closed on main (9002d0f, live)**
**What it is:** The Fly entrypoint takes MUSTER_TOWN_REPO so a self-hosted town pulls from its own fork (gap 2), and monitor FYIs fall back to the Town Hall board when a town has no Prod building (gap 7). Pushed straight to main under Prod's merge rule; reports [dc_fqe1dmlf6b](2026-10-29-self-host-gaps-2-and-7-fixed-on-main-9002d0f-parke-e1dmlf6b.md), [dc_ks5h1tb7zs](2026-10-29-9002d0f-is-live-health-commit-059c7b7-monitor-fres-5h1tb7zs.md). docs/self-host.md strikes both gaps; gaps 1, 3–6, 8, 9 stay open.
**What you'd see:** Nothing changes on muster.town (its repo URL is the default and it has a Prod building). GET /api/health showed the commit containing 9002d0f with monitor lastSampleAt 17 s old and no alerts. API and docs only, no picture. The bring-up proof on a throwaway box still waits on the box and domain in your outbox.
**Your call:** None.

## Decided
- [dc_3deanvehb3](2026-10-29-desk-session-performance-step-1-wall-cpu-steal-per-eanvehb3.md) → approve (desk-perf step 1 merged, b851a0e; live check was the parked continuation)
- [dc_wl5wc54zyb](2026-10-29-desk-perf-step-1-b851a0e-live-and-host-fallback-ve-5wc54zyb.md) → approve (b851a0e live, host fallback verified; parked for a new-image session)
- [dc_ul8l880x7s](2026-10-29-desk-perf-step-1-verified-live-fly-fork-desks-show-8l880x7s.md) → approve (step 1 verified live: 86–91% steal on fork desks, 0.6–13% on Cleo's Machine)
- [dc_eysmkcbp45](2026-10-29-desk-perf-step-2-desk-steal-alert-merged-pr-95-c22-smkcbp45.md) → approve (step 2 merged, PR #95 c229d63; thresholds stay 50/35/25)
- [dc_8ej0m0ycmq](2026-10-29-desk-perf-step-2-live-a-real-desk-steal-red-85-fir-j0m0ycmq.md) → approve (step 2 live: real red 85%, event 57050; FYI wording nit queued as as_x5ifs934vy)
- [dc_yg8gix8gv7](2026-10-29-monitor-step-3-still-waiting-monitor-outbound-is-f-8gix8gv7.md) → approve (monitor test alert park 3 of 3: outbound still false; resumes 10-30 09:20Z)
- [dc_fqe1dmlf6b](2026-10-29-self-host-gaps-2-and-7-fixed-on-main-9002d0f-parke-e1dmlf6b.md) → approve (gaps 2+7 on main 9002d0f)
- [dc_ks5h1tb7zs](2026-10-29-9002d0f-is-live-health-commit-059c7b7-monitor-fres-5h1tb7zs.md) → approve (9002d0f live, monitor fresh, no alerts)
- [dc_id75m3owzu](2026-10-29-session-ended-without-a-report-directory-step-1-re-75m3owzu.md) → approve (directory step 1 fork died without a report; re-queued and finished)
- [dc_ie8yimj67s](2026-10-29-directory-step-1-merged-pr-94-fde6cb2-migration-05-8yimj67s.md) → approve (directory step 1 merged, PR #94 fde6cb2, migration 059)
- [dc_o5qr5a4t8g](2026-10-29-directory-live-check-fde6cb2-live-but-routes-404-d-qr5a4t8g.md) → approve (routes 404'd live; fix PR #98 c2bf441 merged)
- [dc_dgzxfdqhdg](2026-10-29-directory-step-1-is-live-at-c2bf441-all-five-curls-zxfdqhdg.md) → approve (directory step 1 live at c2bf441, five curls pass, Kelly told)

## Key results
| Key result | Grant | Status | Spent / granted |
|---|---|---|---|
| kr_iwj8m0461p town monitor, red alerts reach Mitchell | gr_rntk0echpi | not-started (steps 1–2 live; test alert waits on the outbox secrets, park 3 resumes 10-30 09:20Z) | 346,697 / 800,000 |
| kr_4pf0n8q9jl desk session performance | gr_uhh6u39vv9 | not-started (steps 1–2 live and verified; step 3 waits on your call above) | 264,399 / 700,000 |
| kr_og03nxrkct directory registration | gr_8cdix9mpye | not-started (step 1 live; step 2 queued) | 226,263 / 450,000 |

Today's spend by lane: exploration 86,719 / 828,571 tokens; directed 398,418 tokens.

## Needs from Mitchell
1. Desk steal: say yes or no to step 3 of desk performance as described in Shipped item 1 (auto-move a hot desk to performance-2x, default cap $1/day per building, thresholds kept at 50/35/25). If you want a different cap or no auto-move, say so in words and I'll size the step to that.

_Already waiting in your in-tray: 0 proposals, 3 requests (dc_nwv9dy37ui, dc_nhw4i75len, [dc_nke6xw12k4](../../../../../town-hall/outbox/2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md)), 0 rollups._
