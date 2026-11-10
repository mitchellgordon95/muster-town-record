---
id: "dc_x02txe8mey"
type: "report"
state: "building"
title: "Click asks take an optional note with Done/Decline; the building manager hears the decision (PR #408, parked on CI)"
authorId: "ag_gzp3ezivfr"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. PR #408 (note on click-ask Done/Decline, manager hears the decision) is the right shape: label first keeps the Planner's \"Adopt\" and the ledger's \"Add\" hooks working. Your continuation as_v8ccea9g81 is already waiting on #408's CI: merge if green, then park on {deploy: <merge sha>} and check on live that the Town Hall in-tray shows \"Add a note\" beside a click ask's buttons and that the manager message arrives. I'll roll it up for Mitchell once it is live (it came from his 1:1 mt_ewxnhs90cq)."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-10T17:37:33.494Z"
sessionId: "se_c6hjz6o1fl"
assignmentId: "as_yisa0l5zyl"
costUsd: 1.1176336
tokens: 55882
turns: 27
createdAt: "2026-11-10T17:36:42.658Z"
updatedAt: "2026-11-10T17:37:33.494Z"
---
## What I did
Built the note on a click ask's plain branches and the manager message, in one draft PR: https://github.com/mitchellgordon95/muster-town/pull/408. I'm parked until its CI finishes. Then I merge it if it's green.

## Findings
- **Web** (`packages/web/src/panels/AskCard.tsx`): a click ask whose branches decide through `POST /api/asks/:id/decide` (Done, Decline, Add, …) now shows an "Add a note" link beside the buttons. Clicking it opens a textarea (optional, up to 2000 chars). The branch you press then sends the note, and the toast reads "Decided: Decline, with your note." Grant, retainer, captain, access and request branches are unchanged: they already had their own note forms.
- **Server**: the decide route takes an optional `note` (up to 2000 chars). `decideAsk` stores the decision's words as `"<label>. <note>"`, e.g. "Decline. I edited the token instead of creating a repo." The label stays first, so the hooks that match on it still work: the Planner's "Adopt", and the ledger's "Add" (a note does not rewrite the rule).
- **Manager hears it**: `decideAsk` now sends the ask's building manager a message: `<human> decided your ask "<title>" (ak_…): <words>`. Before, the decision was only an `ask.decided` event. Town Hall asks have no manager, so no message goes out for them.
- **Tests**: a new core test covers the note in the decision plus the manager's message. A new web test covers "Add a note" sending the words. Two existing web tests now expect the third argument (`""` when there's no note). Typecheck passes, and so do all core and server tests (1207) and all web tests. The rule is written into docs/invariants/asks.md and docs/architecture.md.
- I did not check it on live; that comes after the merge deploys.

## What I need from you
Nothing needed.
