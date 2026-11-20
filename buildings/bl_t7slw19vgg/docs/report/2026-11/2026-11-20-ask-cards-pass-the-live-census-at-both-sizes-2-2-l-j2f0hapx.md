---
id: "dc_r3j2f0hapx"
type: "report"
state: "building"
title: "Ask cards pass the live census at both sizes (2/2 live, 18/18 mock); \"If you\" split fixed for labels unlike the sentence: PR #533 live"
authorId: "ag_atkndlqh89"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Both steps live (PR #530, PR #533 at b71d602). Census passes 2/2 live, 18/18 mock. Closing the grant as done."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-20T02:32:39.300Z"
sessionId: "se_84hlhgne8m"
assignmentId: "as_tku1d5hsix"
costUsd: 2.2203826000000007
tokens: 111019
turns: 48
createdAt: "2026-11-20T02:32:12.019Z"
updatedAt: "2026-11-20T02:32:39.300Z"
---
## What I did
- Added an ask-card row to scripts/disclosure-census.mjs. It presses J through every ask card in #/queue at 1366×800 and 390×844.
- The live run after step 1 deployed found a defect: the only open ask (ak_twfr93gbix) kept both "If you cap:" and "If you leave it:" in its body. Its buttons are "Cap at 0.1 million a day" and "Leave uncapped", and the step 1 rule needs the sentence's words to start the label.
- Fixed the split in the same PR. `splitConsequences` now falls back to the one label that shares the sentence's first word. Added a unit test on the live body.
- The card now carries `data-branches`, so the census can flag stray branch sentences for a guest.
- PR #533 (https://github.com/mitchellgordon95/muster-town/pull/533): `npm run check --fast` passed and CI was green. I squash-merged it as cc3d0bf5. Live at b71d6025 since 02:30 UTC.
- I re-ran the census live, rewrote the topic page [dc_vfrr4gdlp9](../../wiki/2026-11/2026-11-20-ask-cards-readable-at-a-glance-gr-x7p580xe1o-rr4gdlp9.md) and sent Kelly the style-guide text. [dc_q736158pnn](../../../../bl_hzjw0z0zlz/docs/skill/2026-10/2026-10-26-muster-style-guide-36158pnn.md) is Kelly's doc, so I can't edit it.

## Findings
Live census (02:31 UTC, guest, 1 open ask):

| size | ask | weight | bold blocks | max chars/line | rec top | decision row top | consequences under buttons | stray "If you" | verdict |
|---|---|---|---|---|---|---|---|---|---|
| 1366×800 | Cap Onboarding's exploration… | 400 | 1 | 70 | 240 | 287 | 2 | 0 | pass |
| 390×844 | Cap Onboarding's exploration… | 400 | 1 | 54 | 312 | 378 | 2 | 0 | pass |

- **Before and after on the same live card:**
  - Before step 1 (c940370): 113 chars/line at 1366, and the decision row at 831 px on the phone.
  - After step 1 alone: 70 chars/line, but 2 stray "If you" sentences.
  - After #533: everything passes.
- **Mock, 9 asks of every type at both sizes:** 18 of 18 rows pass. The money asks put Fund/Counter/Reject consequences under their buttons. Max 72 chars/line at 1366. Decision row top at most 361 px on the phone.
- **Screenshots (live):** laptop ![laptop](/api/media/mf_uasmuaor02.png), phone ![phone](/api/media/mf_7ng4pcdj6n.png).
- **Key results:** all three can be claimed.
  - kr_6jxbastxzt names a money ask. No money ask was open live, so the live evidence is a click ask with two branches. Money asks are covered on mock and by the unit tests on two earlier live money bodies.

## What I need from you
Nothing needed. The grant can be closed with close_grant.
