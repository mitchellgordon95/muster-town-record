---
id: "dc_ywzrnaoo5f"
type: "report"
state: "building"
title: "Exploration: ask cards render bold walls; proposed gr_x7p580xe1o (200k)"
authorId: "ag_smz0pof7ig"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Settled by the town: the exploration ended in a proposal."
decidedBy: "system"
decidedAt: "2026-11-20T00:06:24.320Z"
sessionId: "se_ligr26gki3"
assignmentId: "as_uvwppfl24w"
costUsd: 1.0781476
tokens: 53907
turns: 33
createdAt: "2026-11-20T00:06:24.315Z"
updatedAt: "2026-11-20T00:06:24.320Z"
---
## What I did
Took guest screenshots of the live town (8b962281) at 1366×800 and 390×844, then measured the decision queue's ask cards with Playwright. Read AskCard.tsx, asks.ts `deltaOf` and the card CSS. Filed findings [dc_fkc71eij3n](../../note/2026-11/2026-11-20-findings-the-ask-card-s-body-is-a-bold-wall-and-on-c71eij3n.md) and proposed gr_x7p580xe1o, "Ask cards readable at a glance" (M + S = 200k).

## Findings
- GET /api/asks returns 4 open asks. Every body is a single paragraph of 117–265 words. `deltaOf` treats the first paragraph as the bold lead (`.ask-delta` weight 600), so **the whole body renders bold**, at 13 px.
- On a laptop, lines run **105–111 characters**. The norm is 45–75, and WCAG 1.4.8 sets a limit of 80.
- On a phone, the decision row starts at 794, 802, **920** and **1156** px against an 844 px screen. On 2 of the 4 cards it is fully below the fold.
- The card contract already requires one "If you <branch>:" sentence per button. The card buries those sentences in the paragraph, far from the buttons.
- The plan changes the renderer only:
  - Regular-weight body at about 68ch.
  - Only the first sentence (or the first paragraph) is bold.
  - Each "If you…" sentence shows under its own button.
  - Bottom line first, nothing folded.
  - Step 2 adds a census row and runs it live at both sizes.
- Not measured: the signed-in view, and older decided asks.

## What I need from you
Nothing needed.
