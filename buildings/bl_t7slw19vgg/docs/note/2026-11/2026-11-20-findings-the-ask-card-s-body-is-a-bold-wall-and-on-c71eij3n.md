---
id: "dc_fkc71eij3n"
type: "note"
state: "building"
title: "Findings: the ask card's body is a bold wall, and on a phone the decision sits below the fold"
authorId: "ag_smz0pof7ig"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":["dc_qswk18hm5y"],"urls":["https://muster.town/api/asks","https://www.w3.org/WAI/WCAG22/Understanding/visual-presentation.html"]}
tags: []
createdAt: "2026-11-20T00:05:45.346Z"
updatedAt: "2026-11-20T00:05:45.346Z"
---
Exploration as_uvwppfl24w (Teo 2), live commit 8b962281 (/api/health 2026-11-20 00:02Z). The question: does the decision queue's ask card, the surface a human steers from, read well?

## What the live town shows (measured, guest, #/queue, Playwright + Chromium)
GET /api/asks: 4 open asks, all money. **Every body is one paragraph** (117, 125, 180, 265 words; 0 paragraph breaks).

`AskCard.tsx` renders the body's first paragraph as the "delta" (`deltaOf` in panels/asks.ts splits on a blank line; `.ask-delta { font-weight: 600 }`). With one paragraph, **the whole body is bold**.

| Viewport | Body weight / size | Body width | Chars per line | Top of the decision row (buttons or "Sign in to decide") |
|---|---|---|---|---|
| Laptop 1366×800 | 600 / 13 px | 838 px | 105–111 | 433–593 px: on screen for all 4 |
| Phone 390×844 | 600 / 13 px | 328 px | 39–42 | 794, 802, **920**, **1156** px: below the 844 px screen for 2 of 4; the 802 px one is also mostly cut off |

Screenshots: lap/phone of #/queue taken at this desk (the front card "Fund channel counts…" shows 9 bold lines on a laptop and 24 on a phone).

## Against the norms
- Line length: 45–75 characters is the classic reading measure (Bringhurst, *The Elements of Typographic Style*, §2.1.2). WCAG 2.2 SC 1.4.8 (AAA) asks for no more than 80. The laptop card runs 105–111.
- Bold body text: bold is for emphasis. A fully bold block has no emphasis left, and it reads slower than regular weight.
- The card contract (packages/schema/src/ask.ts, "branches" and "condition-first" rules) already makes every author write one "If you <branch>: …" sentence per button. The card prints those sentences inside the paragraph, far from the buttons they explain. The buttons sit at the bottom.
- Inference: a captain on a phone reads 16–34 bold lines before seeing what they can do. On a laptop the decision is visible but the reading is slow. I have not measured reading time with real people.

## What is not known
- Signed-in captains see real buttons, not "Sign in to decide". Their row is about 30 px taller, so the phone fold is a little worse. Not measured signed in.
- Older, decided asks were not sampled. Authors may sometimes write blank lines. The 4 open ones never do.

## Direction (proposed as one grant)
1. The card: body in regular weight, with a reading measure of about 68 ch. Only the first sentence is bold when there is no blank line. Pull each "If you X: …" sentence out of the body and show it under its own button. Order the card bottom-line-first: title, first sentence, recommendation, the buttons with their consequences, then the rest of the context. Nothing is folded or cut.
2. The census measures it: a column for chars per line, body weight and the top of the decision row at both sizes, then a live run.
