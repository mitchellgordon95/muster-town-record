---
id: "dc_l58rq4xbr7"
type: "report"
state: "building"
title: "Style guide ask-card rules rewritten for PR #546; filed as dc_hi1xvlgvcj for Kelly to paste (a fork can't edit the skill)"
authorId: "ag_p1oloi43kx"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Pasted the body below the ===== line of dc_hi1xvlgvcj into the skill dc_q736158pnn (type skill, state building; the skill's author is me, so the write took). Provenance now also cites PR #546, en_ev179611_relay, mt_gf4un6ct4p, mt_eq521xwgth, dc_hi1xvlgvcj and this report. No live check was possible yet (health at 811c2b5 when you filed); nothing queued for it, the guide cites main 9ba1f937 and the code wins when they disagree."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-11-20T19:26:02.543Z"
sessionId: "se_y6hn50le5d"
assignmentId: "as_g27z7966om"
costUsd: 1.3219370000000006
tokens: 66097
turns: 27
createdAt: "2026-11-20T19:23:02.999Z"
updatedAt: "2026-11-20T19:26:02.543Z"
---
## What I did
- Checked out main at 9ba1f937 (the merge of #546). Read AskCard.tsx, asks.ts, the .ask-* rules in styles.css and disclosure-census.mjs, and checked Teo 1's message against them.
- Rewrote the five ask-card passages of muster-style-guide. My `write` with id [dc_q736158pnn](../../skill/2026-10/2026-10-26-muster-style-guide-36158pnn.md) was refused: "You can only update documents you wrote" (core/src/verbs/docs.ts:258; only installed plugins are exempt). I filed the whole new body as note **[dc_hi1xvlgvcj](../../note/2026-11/2026-11-20-muster-style-guide-rewrite-for-pr-546-paste-into-d-1xvlgvcj.md)** in the filing cabinet instead. Every other section is byte-identical to the 02:37 version.
- Told Teo (ms_tng3k8e3pv). The live check was not done: /api/health shows commit 811c2b5, deploy "current", and main CI on 9ba1f937 is "pending", so #546 is not live yet.

## Findings
The code at 9ba1f937 confirms Teo 1's message, with one correction:
- **Order:** header (AskCard.tsx:159) → title h4 (:163) → deferred stamp (:164) → `.ask-delta` (:165) → `.ask-body` with no `breaks` (:166) → step strip (:167) → Recommends (:168) → claims (:169-173) → one `.ask-actions` row, last (:174-180). Signed out, that row holds "Sign in to decide." (:176).
- **deltaOf** (asks.ts:17-21) returns the first paragraph only; the first-sentence fallback is gone. `splitConsequences`, `.ask-conseq` and `.ask-branch*` no longer exist.
- **CSS:** `.ask-delta, .ask-body { font-weight: 400 }` with no max-width or line-height (styles.css:1111-1115). The 56ch measure is gone. `.ask-actions` is at styles.css:1121-1125.
- **Correction, "no bold text":** this is true for the delta line and the body. Three bold parts remain:
  - the header's kind word, a `<b>` (AskCard.tsx:23-30; styles.css:1106 sets it to 700)
  - the h4 title at the browser's default weight (type.css:17 sets only its size)
  - the claim marks (styles.css:1118)
- **Census:** the ask-card row (disclosure-census.mjs:39-46, :196-231, :275-318) now passes at both sizes on three checks: weight 400, no bold block in the lead or body, and the actions row last holding every button. Characters per line and the recommendation's top are still measured but no longer judged.
- **Guide changes in [dc_hi1xvlgvcj](../../note/2026-11/2026-11-20-muster-style-guide-rewrite-for-pr-546-paste-into-d-1xvlgvcj.md):**
  - The intro now cites 9ba1f937.
  - §11's last Don't now says: no bold in the body, and don't bring back the bottom-line-first layout.
  - §12 "Ask cards" is rewritten. It gives the history (gr_x7p580xe1o, PRs #530/#533, then #541/#542 and #546, 1:1s mt_gf4un6ct4p and mt_eq521xwgth) so nobody reintroduces the layout, the new order with line numbers, and the remaining bold. The "If you <label>:" authoring rule and the phone "rec on first screen" rule are dropped.
  - §13.5's census line names the three pass checks.
  - The "Where things live" line no longer lists `splitConsequences`.

## What I need from you
Kelly: paste everything below the `=====` line of [dc_hi1xvlgvcj](../../note/2026-11/2026-11-20-muster-style-guide-rewrite-for-pr-546-paste-into-d-1xvlgvcj.md) into `write` id [dc_q736158pnn](../../skill/2026-10/2026-10-26-muster-style-guide-36158pnn.md) (type skill, state building).
