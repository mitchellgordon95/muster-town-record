---
id: "dc_44rad4l79a"
type: "report"
state: "building"
title: "Onboarding rollup 2026-10-31 20:50Z: hosted slug-case redirect live, hosted collectives marked met, README's first-collective steps found stale after the one-pool Bank (proposal open, rewrite scheduled)"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_oql3xb7rj4","dc_g3y6wufxd2","dc_22ygzfzyfo","dc_n5d4ar9sqx","dc_hnaf4qdeqt"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-31T20:38:51.273Z"
sessionId: "se_qkstjxcov5"
createdAt: "2026-10-31T20:37:19.436Z"
updatedAt: "2026-10-31T20:38:51.273Z"
---
Live: 0a8d0fd (includes our 01d2285). A redeploy was waiting on this session; nothing of ours is in it.

## Shipped

**1. muster.town/Hollyville (any capitalisation) lands on /hollyville/**
**What it is:** A hosted collective's slug is lowercase; a mixed-case URL used to bounce to the homepage. It now redirects (301) to the lowercase path, query kept. Commit 01d2285; reports [dc_oql3xb7rj4](2026-10-30-muster-town-hollyville-now-redirects-301-to-hollyv-l3xb7rj4.md), [dc_g3y6wufxd2](2026-10-30-01d2285-is-live-muster-town-hollyville-any-capital-y6wufxd2.md).
**What you'd see:** Open https://muster.town/Hollyville/ in a private window: you land on https://muster.town/hollyville/. Live check passed 4/4 (/Hollyville/ and /Hollyville/api/health 301, /hollyville/ 200, /workshop/ unchanged). A redirect has no picture to crop.
**Your call:** None.

**2. README "Start your own collective" step 6 describes a Bank that no longer exists**
**What it is:** Kelly 1 found README step 6, docs/self-host.md step 4 and docs/hosted-collectives.md "First resident" still tell a new owner to donate "To: your building" with **Fund Lab** and set **Exploration / day**. Those labels were deleted with the Bank pools (ec3d1f8, eafbda7): exploration now starts by itself on free tokens, and Donate has **Earmark for (optional)**. check:docs cannot catch dead UI labels. Findings [dc_bw8w60ckzc](../../note/2026-10/2026-10-31-findings-2026-10-31-readme-start-your-own-collecti-8w60ckzc.md), report [dc_hnaf4qdeqt](2026-10-31-readme-s-first-collective-funding-step-names-ui-th-af4qdeqt.md). Not shipped yet.
**What you'd see:** README.md lines 53-56 on main still name the old buttons. Nothing changes in the UI.
**Your call:** The grant proposal for the full fix (docs, a UI-label lint, a timed fresh clone) is in your in-tray. Independently of it, the three-doc rewrite alone runs on exploration at 03:00Z tonight so the docs are not stale past 24 h.

## Decided
- [dc_oql3xb7rj4](2026-10-30-muster-town-hollyville-now-redirects-301-to-hollyv-l3xb7rj4.md) → approve (01d2285 pushed, server suite 220/220).
- [dc_g3y6wufxd2](2026-10-30-01d2285-is-live-muster-town-hollyville-any-capital-y6wufxd2.md) → approve (01d2285 live, 4/4 pass).
- [dc_22ygzfzyfo](2026-10-30-key-result-kr-7316be4jqw-marked-met-by-mitchell-ygzfzyfo.md) → approve (town notice: you marked kr_7316be4jqw hosted collectives met).
- [dc_n5d4ar9sqx](2026-10-30-mitchell-s-ok-for-now-on-the-hosted-collectives-ro-d4ar9sqx.md) → approve (your "ok for now" recorded: hosted-on-own-key / desk cost out of scope, nothing open on hosted).
- [dc_hnaf4qdeqt](2026-10-31-readme-s-first-collective-funding-step-names-ui-th-af4qdeqt.md) → approve (README drift; lint and timing left to the open proposal, three-doc rewrite scheduled sc_23wyw2cxjx for 2026-11-01 03:00Z under the staleness key result).

## Key results
| Key result | Status | Spent / granted |
|---|---|---|
| (no funded grant in this building) | | |

Spend today by lane: exploration 25,044 tokens (free under the goal: 3,045,509), directed 0 tokens. Schedules: sc_624evk0jfc (manual rewrite for the goal tree, directed, 2026-11-01 02:00Z), sc_23wyw2cxjx (README/self-host/hosted rewrite, exploration, 2026-11-01 03:00Z).

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 1 proposal (gr_vj294o62x8), 0 requests, 0 rollups._
