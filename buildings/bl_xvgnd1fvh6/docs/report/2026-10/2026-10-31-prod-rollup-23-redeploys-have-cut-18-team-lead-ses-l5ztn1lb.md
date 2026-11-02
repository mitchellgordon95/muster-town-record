---
id: "dc_tbl5ztn1lb"
type: "report"
state: "building"
title: "Prod rollup #23: redeploys have cut 18 team-lead sessions since 10-29 (~3.9M tokens redone) and page on every deploy; new key result kr_ohom5phapo and a 300k proposal"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_xoazajtr2e","dc_u1zxop6ici","dc_35fodj6v64"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-31T20:00:54.671Z"
sessionId: "se_j23c7wwl9e"
createdAt: "2026-10-31T19:56:52.582Z"
updatedAt: "2026-10-31T20:00:54.671Z"
---
Live: 49afcdd (Workshop's PRs #172/#175/#173; nothing of Prod's went live since #22). Morning check 10-31 clean: backup 04:17Z, monitor fresh, no alerts, desks at 4% of cap.

## Shipped

**1. Finding: every merge to main throws away running team-lead work and pages Wright's pinger**
**What it is:** Cleo 1's exploration ([dc_tx37r2qpkk](../../note/2026-10/2026-10-31-findings-redeploys-cut-host-sessions-18-orphaned-s-37r2qpkk.md), report [dc_xoazajtr2e](2026-10-31-explore-redeploys-cut-team-lead-sessions-18-since-azajtr2e.md)) explains the 8 "sessions failed" board FYIs since 10-30. Every merge redeploys; the drain waits 3 min; team-lead sessions run past that (median 51 s, slowest 10% over 241 s, longest 34 min). At startup the cut sessions are marked `error`, so a planned restart looks like a crash to the monitor, and a red goes through the pinger to your phone. Since 10-29: 18 host sessions "orphaned at restart", 3,936,061 tokens redone (~4.7% of team-lead tokens; one session alone 1.0M). The 20 other errors (desk clusters on 10-31, 5 "success" errors during the credential change) are being characterized by a separate report-only exploration queued now.
**What you'd see:** GET https://muster.town/api/sessions since 10-29: 445 sessions, 38 error, 18 with error "orphaned at restart"; Prod board: [CLEARED] sessions FYIs at 18:06Z 10-30 and 01:27Z 10-31 line up with restart clusters. API-only, no picture.
**Your call:** Keep or cut kr_ohom5phapo (written by Cleo 1 under ob_648ua06ht0); the plan to fix it is the proposal in your in-tray.

## Decided
- [dc_35fodj6v64](2026-10-31-key-result-kr-iwj8m0461p-marked-met-by-mitchell-fodj6v64.md) → approve (your notice: kr_iwj8m0461p marked met 10-31 01:32Z; ob_648ua06ht0 had no open key results until today).
- [dc_u1zxop6ici](2026-10-31-morning-check-2026-10-31-backup-landed-04-17z-moni-zxop6ici.md) → approve (morning check 10-31: backup 27.0 MB at 04:17Z, monitor fresh, alerts empty, desks 4% of cap).
- [dc_xoazajtr2e](2026-10-31-explore-redeploys-cut-team-lead-sessions-18-since-azajtr2e.md) → approve (finding above; follow-up exploration as_emc87fhd5v queued for the desk error clusters).

## Key results
| Key result | Status | Spent / granted |
|---|---|---|
| kr_og03nxrkct directory (gr_8cdix9mpye) | on-track, steps 1-2 live, step 3 deferred by you | ~383k / 450k |
| kr_ohom5phapo restarts don't throw away work or page | not-started (proposal gr_w9ue1k1p0c open) | 0 / 0 |

Today's spend by lane: exploration 36,650 tokens (free under the goal: 5,767,240), directed 0 tokens.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 1 proposal (gr_w9ue1k1p0c), 1 request ([dc_nke6xw12k4](../../../../../town-hall/outbox/2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md)), 0 rollups._

## Key results I wrote (keep or cut: Building → Settings → Key results)
- created kr_ohom5phapo: "A redeploy of muster.town no longer throws away team-lead work or pages anyone: sessions cut by a planned restart end as interrupted (not error) and resume or finish, and the "sessions failed" alert stops firing on deploys" (how to check: GET https://muster.town/api/sessions over the 7 days after the change: zero rows with error "orphaned at restart"; Prod board has no sessions YELLOW/RED FYI within 15 min after a redeploy; from [dc_tx37r2qpkk](../../note/2026-10/2026-10-31-findings-redeploys-cut-host-sessions-18-orphaned-s-37r2qpkk.md))
