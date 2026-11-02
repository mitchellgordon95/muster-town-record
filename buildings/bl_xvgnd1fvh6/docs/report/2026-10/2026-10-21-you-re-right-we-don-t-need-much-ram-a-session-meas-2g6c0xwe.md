---
id: "dc_fv2g6c0xwe"
type: "report"
state: "building"
title: "You're right: we don't need much RAM. A session measures ~1 GB at peak, so an 8–12 GB OVH box (~$9–15/mo) is enough"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":["dc_zlxgeaaa0g","dc_pkv9ky527e","dc_gxtv36rbu6"],"urls":["https://us.ovhcloud.com/vps/"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "i feel like even 1 GB per container is a lot? seems like Claude Code is a big chunk? wondering if there are any hacks we can do to reduce usage here. or, possibly, if multiple agents can share the same desk, and use git worktrees or something"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-21T04:29:58.953Z"
sessionId: "se_6gkqseby6i"
assignmentId: "as_oncd6yua3d"
costUsd: 0.46929639999999995
tokens: 17917
turns: 16
createdAt: "2026-10-21T04:24:52.182Z"
updatedAt: "2026-10-21T04:29:58.953Z"
---
## What I did
My earlier figure of "1–2 GB per session" was an estimate I never measured. This time I measured real memory use inside my own desk container while it ran a live work session, a full `npm run typecheck` and `npm test`. I also checked OVH's smaller plans and filed their prices as a source card: [dc_zlxgeaaa0g](../../../../../library/source/2026-10/2026-10-21-source-ovhcloud-us-vps-2027-lineup-prices-fetched-xgeaaa0g.md). There were no code changes and no redeploy.

## Findings
**You're right, it isn't intense.** Here is what one work session uses, from the container's own memory counters:
- **Each session is already capped at 2 GiB.** That limit is set on every desk container.
- **About 0.4 GB while working normally.** Claude Code takes about 285 MB and the desk runner about 100 MB.
- **About 1.0 GiB at the heaviest moment.** That's the typecheck, which ran for 12.8 s. The test suite peaked at about 0.85 GiB. Most of a session sits near the 0.4 GB level.
- **The server itself:** I couldn't measure it from a desk. My guess is 0.2–0.5 GB for Node plus SQLite at our size. Add about 0.5 GB for Linux, Docker and Caddy.

**So the real requirement is:** about 1 GB plus about 1 GB per session running at the same time (it's usually 0.4 GB).
- Typically 2 sessions overlap, which needs about 3 GB.
- The busiest workshop hour had 5 overlapping, which needs about 6 GB.

**Where the big numbers came from:**
- **16 GB was Wright's condition for sharing his box, not what we need.** His box already runs MiniClaw and his own Claude sessions. One of those ran away to 7.4 GB yesterday. That wasn't one of ours. He wanted headroom so that our work could never crowd out your SMS assistant.
- **24 GB was never a requirement either.** It's simply what OVH's VPS-4 includes at $27.50. I picked it for room to grow and should have said the smaller plans would do.

**Cheaper OVH US plans that fit** (prices from OVH's page, apparently for a 12-month commitment):
- **VPS-2: 4 vCPU / 8 GB / 75 GB for $8.50/mo.** That covers about 5 sessions at peak.
- **VPS-3: 6 vCPU / 12 GB / 100 GB for $12.32/mo.** That's comfortable, with room for busier days.
- **Without a commitment:** I estimate about $10 and about $14.50/mo, assuming the same ~18% markup as VPS-4. I haven't seen those prices quoted.
- **Upgrading later:** OVH lets you move up to a bigger plan, so starting small is low-risk.

**My recommendation now:** VPS-3 (12 GB), or VPS-2 if you'd rather spend as little as possible. Either way, total cost would be about $13–18/mo including the domain, instead of $28–35.

**Side note:** while measuring, `npm test` exited with code 1. The parts I saw passed (33 tests), so I don't know what failed. It didn't affect the memory figures.

## What I need from you
Order an OVH US VPS-3 (or VPS-2) with Ubuntu 24.04 in Oregon, add an SSH key we can use, and create a Cloudflare R2 bucket.

## Reply from Mitchell (2026-10-21 00:29)

i feel like even 1 GB per container is a lot? seems like Claude Code is a big chunk? wondering if there are any hacks we can do to reduce usage here. or, possibly, if multiple agents can share the same desk, and use git worktrees or something

