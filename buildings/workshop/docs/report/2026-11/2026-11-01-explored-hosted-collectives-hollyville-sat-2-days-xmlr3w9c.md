---
id: "dc_vhxmlr3w9c"
type: "report"
state: "building"
title: "Explored hosted collectives: Hollyville sat 2 days with 0 sessions; proposed gr_5ltmbf3a2f (own tree, first building, first exploration on the founder's key)"
authorId: "ag_qy9mcaa2ry"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_ptei1pdy99","dc_pl034gahw2"],"urls":["https://muster.town/hollyville/api/goals","https://muster.town/hollyville/api/events?limit=200"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Done: findings dc_ptei1pdy99 and topic page dc_pl034gahw2 stand; gr_5ltmbf3a2f reaches Mitchell in the Town Hall in-tray on its own (its note already asks whether Hollyville should change or only new collectives). No further assignment until he funds, counters or rejects it."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-01T01:23:47.259Z"
sessionId: "se_j80pi62iov"
assignmentId: "as_ke726wnt4f"
costUsd: 1.0705527999999997
tokens: 53528
turns: 29
createdAt: "2026-11-01T01:23:32.864Z"
updatedAt: "2026-11-01T01:23:47.259Z"
---
## What I did
I took one direction under gl_jktf4bngcu: what happens after a stranger presses "Start a collective". I read the live hosted collective through its public API, traced the seed code (hub.ts, seed.ts, goals.ts, migration 061, explore.ts), and seeded a hosted-style World locally to confirm. Findings are in [dc_ptei1pdy99](../../note/2026-11/2026-11-01-findings-a-hosted-collective-stalls-at-birth-holly-ei1pdy99.md) and the topic page is [dc_pl034gahw2](../../wiki/2026-11/2026-11-01-hosted-collectives-first-run-034gahw2.md). I made no code changes.

## Findings
- **The only hosted collective has stalled.** Hollyville was started by @edwadli on 2026-10-29 at 23:06Z. Mitchell joined and the two exchanged a couple of chat lines. Since then the event log has nothing but daily resets: zero sessions on 10-30 and 10-31, no API key, no building except the Town Hall, and no resident.
- **Its goal tree belongs to the Workshop, not to the founder.** The root reads "Make money", but under it sit the Workshop's Fund/Join/Trust pillars, and the captain is "the town admins". Migration 061 adds those pillars to every database, hosted ones included.
- **Why no work starts:** a new collective gets no building (`buildings: []`, hub.ts:113). The explore tick only starts work in a building with a free desk, so it has nowhere to run.
- **The money would be there.** If the founder had added a key, the Start form credits 1,000,000 tokens. That leaves 500,000 free after the reserve, enough for the 100,000-token exploration chunk.
- **Proposed grant gr_5ltmbf3a2f** (400,000 tokens, three key results due 11-04 to 11-06):
  1. The founder's own tree: their goal at the root, them as captain, no pillars. This also retires Hollyville's three empty pillars.
  2. Starting a collective creates a first building with a resident at a desk. A founder without a key sees one step: "Add your API key to start".
  3. With a key, an exploration starts on its own and a grant proposal reaches the founder's in-tray within an hour, billed to their key.
- It depends on decision 7 (as_mnahvr6rn8, the root goal always has a captain).
- **Not yet confirmed:** that the hosted runtime actually runs the explore tick. Its stop condition covers the case where it can't.

## What I need from you
Decide gr_5ltmbf3a2f. Key result 1 changes Edward's live collective (Hollyville), so tell me if only new collectives should change.
