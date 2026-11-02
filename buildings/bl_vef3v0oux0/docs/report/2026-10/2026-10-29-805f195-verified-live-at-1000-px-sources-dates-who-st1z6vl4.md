---
id: "dc_srst1z6vl4"
type: "report"
state: "building"
title: "805f195 verified live at 1000 px: Sources dates whole, ranges wrap after the arrow, labels read as words, Spending unchanged, Total received ✓ 52,729,370; no regression, no code change"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":["dc_i3v16qy7in","dc_0yo2agaodj"],"urls":["https://muster.town/workshop/?guest#/finance"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "805f195 verified live at 1000 and 1400 px; the gr_gbpbbwy9b8 layout follow-up is closed, kr_j9058i256a stays claimed pending Mitchell's call on dc_0yo2agaodj. Nothing further on this key result."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-10-29T01:32:06.845Z"
sessionId: "se_1qqum45fk5"
assignmentId: "as_81u35pdx5s"
costUsd: 1.30821115
tokens: 26164
turns: 17
createdAt: "2026-10-29T01:31:50.263Z"
updatedAt: "2026-10-29T01:32:06.845Z"
---
## What I did
Confirmed GET /api/health reports commit 805f195 (2026-10-29 01:29Z). Ran a Playwright check (~/shots/verify805.mjs) against https://muster.town/workshop/?guest#/finance at 1000 px and 1400 px viewports: measured every Sources row's label and date column, dumped the client rects of the date spans, printed the three "Adds up" lines, and screenshotted the Sources and Spending sections. Reviewed the pictures. No code change this session; nothing to commit.

## Findings
All four checks from the assignment hold at 1000 px (panel 327 px wide):
- **Dates whole.** Every `.spend-date` is `min-width: auto` and each `.day` span is `white-space: nowrap`; single dates render on one line, 73 px wide. No "2026-" / "10-21" split anywhere.
- **Ranges wrap after the arrow.** The third input shows "2026-10-21 →" on one line (both text fragments at the same y, x 799–886) and "2026-10-26" right-aligned on the next line. Same for the 2026-10-25 → 2026-10-26 and 2026-10-27 → ranges.
- **Labels still words.** Input labels are 120–134 px wide and break at spaces ("Mitchell's Claude subscription (Max 5x): ~80% of the weekly plan estimated from…" reads as words). At 1400 px the panel is 467 px and everything fits on fewer lines.
- **Spending unchanged.** Rows by building with session counts, amounts and shares as before; "Weight mismatch" and "Not funded" rows intact; ✓ "the rows sum to used, 33,877,727".
- **Total received ✓ 52,729,370** = credited 48,099,993 + donated 4,629,377, matching the Tokens section's total; Tokens ✓ line also present (used 33,877,727 + expired 11,120,685 + left 8,264,998 = total 52,729,370 + overdrawn 534,040).

The 090c169 + 805f195 layout follow-up to the gr_gbpbbwy9b8 close is done. kr_j9058i256a stays claimed, awaiting Mitchell's met/missed from the close rollup [dc_0yo2agaodj](2026-10-29-bank-transparency-gr-gbpbbwy9b8-closed-as-done-fun-o2agaodj.md). Nothing open on this key result.

## What I need from you
Nothing needed.
