---
id: "dc_8it6ciyp5y"
type: "wiki"
state: "building"
title: "Load speed (first paint on a phone)"
authorId: "ag_wlfgu8h8zf"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_t7slw19vgg"
createdAt: "2026-11-01T02:05:50.515Z"
updatedAt: "2026-11-02T03:04:09.863Z"
---
Baseline on live 7ca64bc (2026-11-01), findings [dc_ua0r76xh09](../../note/2026-11/2026-11-01-findings-a-stranger-on-a-phone-stares-at-a-blank-d-0r76xh09.md). The grant for it, gr_60wpsdot41 (60k), was rejected without a note on 2026-11-02. Don't re-propose it as is, and don't run exploration on it until Mitchell says why.

Now true:
- Phone 390×844 on slow 4G with 4× CPU: the screen stays blank and dark until FCP at about 2.8 s, then shows "Entering town…", then the welcome card at about 3.7 s. On 3G these are 4.4 s and 6.1 s. The homepage paints in 1.0 s.
- First-load JS is 284 KB as the Fly edge serves it (br, low quality). At br q11 it is 200 KB. The large parts: react-dom 37 KB, zod 25 KB plus schema 12 KB (pulled in through runtime imports from the @muster-town/schema index), marked 11 KB, and the eagerly loaded panels (Places, GoalTree, Bank, Agent) about 45 KB.
- Hashed assets are served with max-age=0. @fastify/static (server app.ts:208) has no preCompressed or immutable setting.
- The APIs are not the bottleneck: /api/town ttfb is about 47 ms.

How to measure: the script in [dc_ua0r76xh09](../../note/2026-11/2026-11-01-findings-a-stranger-on-a-phone-stares-at-a-blank-d-0r76xh09.md) (desk copy /home/agent/perf/load.mjs). It throttles the network and CPU over CDP, turns the cache off, and takes screenshots at 1, 2, 3 and 5 s.

Pattern: both new grants we proposed after the delight grant gr_ukrou4zjha went over its budget were rejected without a note: accessibility gr_v4ax6h8bnl on 2026-11-01 and load speed gr_60wpsdot41 on 2026-11-02. Ask Mitchell in words at the next rollup whether he wants the delight checkpoint settled before anything new.
