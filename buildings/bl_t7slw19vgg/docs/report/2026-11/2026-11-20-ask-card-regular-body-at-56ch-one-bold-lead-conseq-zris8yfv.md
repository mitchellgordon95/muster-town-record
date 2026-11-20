---
id: "dc_nnzris8yfv"
type: "report"
state: "building"
title: "Ask card: regular body at 56ch, one bold lead, consequences under buttons: PR #530 parked to merge"
authorId: "ag_m6fa1edhwy"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-20T01:50:00.996Z"
sessionId: "se_49mc17d5nu"
assignmentId: "as_hwxw0uv6fb"
costUsd: 1.7946755000000003
tokens: 89734
turns: 45
createdAt: "2026-11-20T01:50:00.943Z"
updatedAt: "2026-11-20T01:50:00.996Z"
---
## What I did
Changed AskCard.tsx, asks.ts and styles.css. Added `splitConsequences` and a new `deltaOf` lead rule, with unit tests on the two live bodies from GET /api/asks at 01:41 UTC (only 2 were open; both were decided by 01:43). Took screenshots of the mock at 1366×800 and 390×844, with a live body swapped into a fixture ask (not committed). Opened PR #530 (https://github.com/mitchellgordon95/muster-town/pull/530) and parked it to merge when green. `npm run check --fast` passes: 131 tests, typecheck, deadcode, docs.

## Findings
- **Order:** title, lead, recommendation, buttons, each with its "If you …" sentence under it, rest of the body, step strip, claims. Signed out, each consequence shows under the branch's name, followed by "Sign in to decide."
- **Lead:** only the lead is bold (weight 600). It is the first paragraph when the body has a blank line, else the first sentence. The body is weight 400 with line-height 1.5. Single newlines now render as line breaks, not as one run-on paragraph.
- **Line length:** a max-width of 68ch gave 84 characters per line at 1366. 60ch gave exactly 80. **56ch gives at most 75** (measured from the character rects of the lead, the body and the consequences).
- **Phone (390×844):** the recommendation starts at 331 px and the decision row at 378 px. Lines are at most 56 characters.
- **The split:** "If you counter at 50k:" goes to Counter, and "If you add it:" goes to Add. "If you agree, reply Bar" has no colon, so it stays in the body. "If you claim:" on a card whose buttons are Done and Decline stays in the body too. On both live bodies all three sentences went to the right button, and nothing was misplaced.
- Topic page [dc_vfrr4gdlp9](../../wiki/2026-11/2026-11-20-ask-cards-readable-at-a-glance-gr-x7p580xe1o-rr4gdlp9.md) has the details for step 2. The live check needs at least one open ask, and the queue was empty at 01:43 UTC.

## What I need from you
Nothing needed.
