---
id: "dc_cs6me6go5r"
type: "report"
state: "building"
title: "PR #408 widened to outbox requests (Claim note, Decline note) and CI fix pushed; parked on CI"
authorId: "ag_soo3n63wyh"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved. Parked continuation stands: when CI on 79a4fed5 finishes, mark #408 ready and merge if green (no redeploy), park on its deploy, then live-check a click ask's note and a request ask's Claim note and say who received the words. Rollup follows once it is live."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-10T17:50:14.731Z"
sessionId: "se_rr6z6it708"
assignmentId: "as_v8ccea9g81"
costUsd: 0.9922718
tokens: 49614
turns: 25
createdAt: "2026-11-10T17:50:04.643Z"
updatedAt: "2026-11-10T17:50:14.731Z"
---
## What I did
PR #408's first CI run failed: knip flagged the unused export `decisionWords`. I un-exported it. Teo then relayed Mitchell's line from 17:38 ([dc_fyox7jmhdh](2026-11-10-message-from-mitchell-via-secretary-teo-widen-as-y-ox7jmhdh.md)), so I widened #408 to cover outbox-request asks. Pushed 79a4fed5. I'm parked until CI on it finishes.

## Findings
- **Web**:
  - A request ask's buttons now read **Claim…** and **Decline…**, and each opens a note field.
  - Claim's note is optional. The placeholder reads "optional: how you'll do it, e.g. use Wright's VPS". With a note, the toast says "Claimed, with your note: the author hears it."
  - Decline's note is required: the button stays disabled until something is typed. Before this, the card's Decline sent no note, and the server refuses a decline without one (ops.ts "Say why you decline it"), so Decline failed on live.
- **Server** (`requestAction`, case `claim`):
  - The trimmed note is stored as `requestNote`.
  - The agent author always gets a system message: `<human> claimed your outbox request "<title>" (<id>): <note>`. With no note, the line ends with a period.
  - The `doc.updated` event text includes the note on a claim when one was given.
- **Tests**:
  - New core test in wakes-step5: note stored, author messaged in both cases, note in the event.
  - New web test: Decline stays disabled until a note is typed; Claim works empty and sends the note.
- **Checks passed**:
  - Typecheck and the knip, docs and css checks.
  - All 414 web tests.
  - These core suites: asks, wakes-step5, verbs, work-routing-step2 and act-in-1on1.
- docs/invariants/asks.md now covers request Claim and Decline.
- Next, once CI is green: mark #408 ready and merge it (no redeploy), then park on its deploy. After that, check on live both a click ask's "Add a note" and a request ask's Claim note, and report who received the words.

## What I need from you
Nothing needed.
