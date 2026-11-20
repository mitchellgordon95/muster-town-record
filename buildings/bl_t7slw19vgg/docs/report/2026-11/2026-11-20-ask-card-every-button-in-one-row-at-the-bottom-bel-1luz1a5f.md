---
id: "dc_851luz1a5f"
type: "report"
state: "building"
title: "Ask card: every button in one row at the bottom, below the text: PR #542, parked to merge when green"
authorId: "ag_9cv89fuz94"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "stop"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-20T18:28:43.559Z"
sessionId: "se_xn3ysqgc6l"
assignmentId: "as_aqsosz9n1z"
costUsd: 1.3687807999999997
tokens: 68439
turns: 30
createdAt: "2026-11-20T18:28:43.544Z"
updatedAt: "2026-11-20T18:28:43.559Z"
---
## What I did
Mitchell asked for this in 1:1 mt_gf4un6ct4p. I moved every action on the ask card back into one row at the bottom of the card. PR https://github.com/mitchellgordon95/muster-town/pull/542 is parked to merge when green.

## Findings
- **New card order (AskCard.tsx):** header, title, deferred stamp, bold lead, recommendation, the whole body, step strip, claims. Then one `.ask-actions` row comes last. It holds the branch buttons, the aside, Steer and "The full record →". The counter / adjust / note form still opens right under the buttons. Signed out, the same row says "Sign in to decide." (or "A captain or admin decides this.").
- **"If you <branch>:" sentences** now stay in the body where the author wrote them. I removed `splitConsequences` (asks.ts), the `consequences` prop, the old tests and the dead CSS: `.ask-branch`, `.ask-conseq`, `.with-conseq`, `.ask-branches-static` and `.ask-foot`. The bold lead and the 56ch / line-height 1.5 body are unchanged. The `deltaOf` tests moved to test/askLead.test.ts. The card tests now check three things: the row is the card's last element, it is the only row, and every button on the card is inside it (Fund, Counter…, Reject, Steer, The full record).
- **Census:** the ask-card row in scripts/disclosure-census.mjs no longer flags "If you" sentences in the body or checks that the decision row is above the fold. At both sizes it now checks that the row is the card's only and last block, with nothing laid out below it and no button outside it. The weight, bold-block and chars-per-line checks are unchanged. Mock result: **18/18 pass** at 1366×800 and 390×844. Screenshots: mf_afwdyqff0o (laptop), mf_2dpyl5z4ql (phone). I did not run it live: the live site still serves the old card until #542 deploys.
- **`npm run check`:** docs, deadcode and typecheck pass. 1132 of 1133 tests passed. The one failure was packages/core export-import "off the main thread", which timed out at 5 s under load. It passed 9/9 when run alone. It has nothing to do with this change.
- **Other updates:** I told Kelly (ms_8cpmzg7fd3) to update the ask-card section of muster-style-guide [dc_q736158pnn](../../../../bl_hzjw0z0zlz/docs/skill/2026-10/2026-10-26-muster-style-guide-36158pnn.md). She is idle, so she will see it in her next session. I rewrote topic page [dc_vfrr4gdlp9](../../wiki/2026-11/2026-11-20-ask-cards-readable-at-a-glance-gr-x7p580xe1o-rr4gdlp9.md) and added the log entry docs/log.d/2026-11-20-ask-card-all-buttons-in-one-row-at-the-b.md.

## What I need from you
Nothing needed.
