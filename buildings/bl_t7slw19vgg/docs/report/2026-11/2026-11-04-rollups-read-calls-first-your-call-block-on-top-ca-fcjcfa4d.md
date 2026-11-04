---
id: "dc_rqfcjcfa4d"
type: "report"
state: "building"
title: "Rollups read calls first: \"Your call\" block on top, cards next, Decided / Key results / provenance folded; Needs lines reach the deck slide (PR #327, parked on CI)"
authorId: "ag_s1kuuuo54b"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":["mt_i50xwu4z2t","dc_6hza7i15p4","dc_mk6wtf0yrn"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/327"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Parked work already resumed on its own as as_zi7zszpy17 (merge #327 if green, redeploy, verify on live at both sizes, roll up). Nothing more to queue."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-04T18:56:59.125Z"
sessionId: "se_ogm67n28u7"
assignmentId: "as_igsg6x1v1z"
costUsd: 6.363668749999999
tokens: 318183
turns: 66
createdAt: "2026-11-04T18:55:29.070Z"
updatedAt: "2026-11-04T18:56:59.125Z"
---
## What I did
Mitchell's ask from 1:1 mt_i50xwu4z2t ("the reports themselves are still hard to read"), under the progressive-disclosure goal gl_1ds3wl2n78. Draft PR #327: https://github.com/mitchellgordon95/muster-town/pull/327 (typecheck green, the rollup, deck, prompt and web tests pass; the one red in `npm run check --fast` was the backup worker-thread timing test, which passes alone).

- **Report view (UI / UX's own):** a rollup opened from the Town Hall in-tray now opens on a "Your call" block that quotes every Shipped item's real call and the Needs lines (or says "Nothing to decide" when all are None), then the Shipped cards (a None call shows no gold line), then Decided, Key results and provenance folded under one click each. `RollupReport` in packages/web/src/panels/RollupCards.tsx; DocView folds provenance for every doc.
- **Parser (schema):** `parseRollup().sections` (Decided / Key results / Needs split out) and `rollupAsks()` (the lines a human must decide, in reading order; "None", "Nothing needed" and the generated waiting line left out). `rollupWarnings` warns when "What it is" runs over 80 words.
- **Review deck (core):** a rollup's Needs lines ride on its first slide, or make its one slide (`rollup:<id>:needs`) when no item asks a call. Before, a Needs line that had no other channel (a question in words) never reached the deck or the digest.
- **Format rule managers write to (core prompts.ts, touches every manager's prompt once):** the template now says how a rollup is read (calls and cards stand alone; Decided / Key results are folded, so no prose there; "What it is" two or three sentences under 80 words). Headings and labels are unchanged, so every existing rollup still parses.
- Mock rollup dc_moss_rollup rewritten in the labelled format; told Pix (ms_iw4kr3ay04) to source the digest's "Decisions needed" from `rollupAsks` so the card and the report quote the same lines, Needs included. Topic page [dc_6hza7i15p4](../../wiki/2026-11/2026-11-04-rollup-report-view-calls-first-za7i15p4.md).

## Findings
Mock Town Hall in-tray, the same two-item rollup with one real call, laptop 1280×800 (phone 390×844 the same):

| | first screen | screens | where the call sits |
|---|---|---|---|
| before | 2 controls, 160 words | 1.9 | last, under the second card |
| after | 2 controls, 175 words | 1.4 | first line |

![after](/api/media/mf_tszb2vjzkb.png)

What was overloading: every rollup section was rendered in full in writing order (intro, cards, an 8-line Decided list, a 4-column key-results table, Needs, then a provenance list of 8 titles), and the one thing Mitchell needs, the call, came last. Real rollups like my checkpoint [dc_mk6wtf0yrn](2026-11-04-checkpoint-progressive-disclosure-grant-at-401-202-6wtf0yrn.md) run 3+ screens with the call at the bottom.

## What I need from you
Nothing needed (I merge #327 when CI is green, redeploy, verify on live and roll it up with gr_zak30564zh steps 3–4; the rollup will say the manager prompt template changed for every building).
