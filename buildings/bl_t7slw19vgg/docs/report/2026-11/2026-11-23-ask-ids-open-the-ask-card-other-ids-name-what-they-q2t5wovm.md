---
id: "dc_yoq2t5wovm"
type: "report"
state: "building"
title: "Ask ids open the ask card; other ids name what they are: PR #575, parked to merge when green"
authorId: "ag_mevwo58fcl"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-23T16:36:39.493Z"
sessionId: "se_3aug9lmwve"
assignmentId: "as_97il0i1rlx"
costUsd: 1.8591595999999997
tokens: 92958
turns: 41
createdAt: "2026-11-23T16:36:39.455Z"
updatedAt: "2026-11-23T16:36:39.493Z"
---
## What I did
Changed id linking in packages/web/src/panels/Markdown.tsx, LinkSheet.tsx, AskCard.tsx (new `readOnly` prop), route.ts and state.ts. Also added `?peek=1` to GET /api/asks/:id in packages/server/src/routes/asks.ts. Opened PR #575 (https://github.com/mitchellgordon95/muster-town/pull/575). `npm run typecheck` passes. Web tests pass (95 files, 488 tests), and server test/asks.test.ts passes. Topic page: [dc_vtd08xjagx](../../wiki/2026-11/2026-11-23-every-id-reads-as-its-name-gr-4upa0og9zc-d08xjagx.md).

## Findings
- **ak_ ids** now read as the ask's title, clipped to 48 characters. The tooltip reads "ask ak_…: full title".
  - The title is fetched with GET /api/asks/:id?peek=1. The new peek mode writes no seen row and does not re-run claim checks, so labelling a link does not count as the human having seen the ask.
  - A click opens the card read-only in the link sheet (hash `#/ask/<id>`).
  - When the ask is closed, the sheet shows a line saying what became of it (decided by whom and how, folded, or closed). A folded ask also links to the ask it was folded into. While the ask is open, the sheet links to the decision queue.
- **sc_ and gp_ ids** open what they belong to, using /api/scheduled and /api/goal-proposals (each fetched once).
  - A schedule opens its grant, or its building if it has no grant.
  - A goal proposal opens its result goal, else its target, else its parent.
  - An id the API doesn't return stays muted. Ended schedules are not in /api/scheduled, so their ids stay muted.
- **en_, ms_, us_, ob_, rs_, nt_ and cr_ ids** are now muted spans, not raw text. The tooltip says what each is, for example "thread entry en_…: opens nothing here".
- **Check against the weekly pattern report [dc_ntd2iabhpg](../../../../town-hall/docs/report/2026-11/2026-11-23-weekly-pattern-note-2026-11-23-nt-cidh52f9ns-filed-d2iabhpg.md):** I used its real text (7 ak_, 2 nt_, 1 ms_, 1 gr_) as a test, not a browser check on the mock. The mock has no such doc. The test shows ak_74axg6n1ke rendering as a named link to its card, and nt_ and ms_ as muted spans with tooltips.
- Not checked on the live town yet. That is step 3, along with the census. The census should count muted ids as "names what it is", not as dead.

## What I need from you
Nothing needed.
