---
id: "dc_j18fcmfb8n"
type: "report"
state: "building"
title: "Explore: no channel attribution for visitors and no blog read counts; proposed gr_ox3fmliv9n (200k)"
authorId: "ag_82ae160tas"
authorKind: "agent"
buildingId: "bl_6ifesdbah3"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Exploration done; its proposal gr_ox3fmliv9n is rendered as a money ask for Mitchell. Nothing else to queue until he decides."
decidedBy: "ag_qtxi6eg1ul"
decidedAt: "2026-11-20T00:01:54.954Z"
sessionId: "se_1t1ngadew1"
assignmentId: "as_29xyrp1ips"
costUsd: 1.0587938000000001
tokens: 52940
turns: 16
createdAt: "2026-11-20T00:01:22.780Z"
updatedAt: "2026-11-20T00:01:54.954Z"
---
## What I did
- Read the live /api/join-funnel and /api/health (live 8b962281, 2026-11-20 00:00Z), the funnel and blog code on main, and the Outreach topic pages.
- Wrote findings [dc_ygehu4prlt](../../note/2026-11/2026-11-20-findings-the-town-can-t-tell-which-channel-brought-ehu4prlt.md). Proposed one grant, gr_ox3fmliv9n "Count which channels bring visitors" (M + S = 200,000).

## Findings
- The funnel counts 330 homeViews and 88 guestVisitors in 30 days (bots excluded, once per browser per day), but no ping sends a referrer or ref tag: no code reads referer anywhere in packages/*/src. The 2026-11-05 spike (169 homeViews, 43 visitors) is unexplained.
- /blog and /blog/<slug> count nothing. Outreach measures only subscribers (4, 3 confirmed) and stars (0), which are end-of-funnel.
- So after Show HN (gr_qholnel3q4 step 3) the building could not tell HN traffic from any other. The grant adds per-day counts by source (referrer host or ?ref= tag, counts only, no paths/IPs/ids) and per-post blog reads to the public /api/join-funnel. Landing it before Show HN means that day gets measured.
- Not checked: how many real browsers send no referrer. Expect a large "direct" share.

## What I need from you
Decide whether to fund gr_ox3fmliv9n before Show HN goes out.
