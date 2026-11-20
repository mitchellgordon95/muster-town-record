---
id: "dc_o85fn19jzc"
type: "report"
state: "building"
title: "PR #547 closed as a duplicate of #546 (merged); ask card has no bold, buttons at bottom"
authorId: "ag_n818u3ji0k"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Settled by the town: the request is done."
decidedBy: "system"
decidedAt: "2026-11-20T19:18:53.029Z"
sessionId: "se_8vsgpn3tsh"
assignmentId: "as_law0558f3e"
costUsd: 0.5897321999999999
tokens: 29487
turns: 16
createdAt: "2026-11-20T19:18:53.023Z"
updatedAt: "2026-11-20T19:18:53.029Z"
---
## What I did
#547's red check was `image`. The Docker build failed with "fatal: not a git repository" at the Dockerfile's gitdir step, which is a CI infra fault: `check` passed and the change itself was fine. I then found that #546 (Teo 1, as_4e78xs5bkq) does the same revert for the same 1:1 (mt_eq521xwgth) and was green. I closed #547 as superseded with a comment, and #546 merged at 19:17:44Z (GitHub). I rewrote topic page [dc_vfrr4gdlp9](../../wiki/2026-11/2026-11-20-ask-cards-readable-at-a-glance-gr-x7p580xe1o-rr4gdlp9.md) and sent Kelly a correction for [dc_q736158pnn](../../../../bl_hzjw0z0zlz/docs/skill/2026-10/2026-10-26-muster-style-guide-36158pnn.md).

## Findings
- The two PRs differed in one item only. #547 kept the first paragraph bold at 600. #546 makes all ask-card text weight 400, and `deltaOf` goes back to "first paragraph". #546 is the more literal reading of Mitchell's words: "ok with everything else except the bold".
- Everything else is the same in both PRs and is now on main. The 56ch width, line-height 1.5, single-newline breaks and the lead→rec→body order are reverted. The buttons stay in one `.ask-actions` row at the bottom. The census fails any bold block.
- What a human will see live: an ask card like the one before the grant, with full-width regular text and the recommendation after the step strip. No text on the card is bold, and every button sits in one row at the bottom.
- If Mitchell wants the bold first line back, it is a one-line CSS change (`.ask-delta { font-weight: 600 }`).
- The duplicate happened because two directed assignments came from the same 1:1: as_4e78xs5bkq (via the Secretary) and as_f4kqtym14o (via Teo).

## What I need from you
Nothing needed.
