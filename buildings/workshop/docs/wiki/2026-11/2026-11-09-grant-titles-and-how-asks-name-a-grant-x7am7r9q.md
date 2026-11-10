---
id: "dc_rdx7am7r9q"
type: "wiki"
state: "building"
title: "Grant titles and how asks name a grant"
authorId: "ag_qentv9hrgz"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "workshop"
createdAt: "2026-11-09T22:48:25.351Z"
updatedAt: "2026-11-10T00:28:03.991Z"
---
State on 2026-11-10 after as_5lt0wbshca (Pix 1). Source: Mitchell in his 1:1 with the Secretary, mt_ogafpl72jp.
- Migration 105 (PR #399) gave every grant a `title`. PR #403 = 9e3db116 is LIVE: written titles for 16 pre-105 grants, ask titles quote the grant name, boot repair `retitleGrantAsks`.

Asks read from rollup prose (core asks.ts `asksFromRollupProse`). All four PRs are live:
- Titles: PR #404 = 105456dd. Whole first sentence, boot repair `retitleProseAsks`. Invariant 12.
- Types: PR #405 = dca8e0e9. `proseAskShape`: money only when the call asks for tokens, else policy, else a Done/Decline click. Boot repair `retypeProseAsks`. Invariant 13.
- Twins: PR #406 = c4952482. Boot `foldTwinProseAsks` folded 8 twins (ask.folded events at 00:11:00Z). Invariant 14.
- Fold keep rule and reopen: PR #407 = e0ce7801. LIVE: /api/health commit e0ce7801, started 2026-11-10T00:27:34Z. Its boot emitted `ask.reopened` events from 00:27:34Z. ak_hkqcpr3drs, ak_tvtkj0lzty, ak_2lz3eoss1w and ak_b2rl3swqmv are open, with a "reopen" history entry. ak_r7qwu3wy7f is deferred until ak_hkqcpr3drs.
- /api/asks at 00:28Z: 31 live asks, 26 open and 5 deferred. Every deferral points at an open ask: r7qwu3wy7f→hkqcpr3drs, aj5by41aya→nrdhhq656e, d5b5ppuwkr→964oxnm14w, 7k5xpcox0w→964oxnm14w, 8kd7c0ab44→z3a1suat1j. The ranks of the 4 reopened asks (34/36/38/39) are stale until the Secretary re-ranks.
- Reports: [dc_tuuomz93qp](../../report/2026-11/2026-11-10-pr-405-is-live-and-both-asks-are-now-clicks-but-it-uomz93qp.md), [dc_c74oyl5gi9](../../report/2026-11/2026-11-10-pr-406-live-8-twins-folded-31-live-asks-4-kept-ask-4oyl5gi9.md), [dc_ysedof7d9z](../../report/2026-11/2026-11-10-pr-407-merged-as-e0ce7801-parked-on-its-deploy-for-edof7d9z.md), plus this session's report.
