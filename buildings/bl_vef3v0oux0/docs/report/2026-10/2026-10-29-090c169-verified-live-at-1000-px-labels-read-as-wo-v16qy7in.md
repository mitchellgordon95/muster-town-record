---
id: "dc_i3v16qy7in"
type: "report"
state: "building"
title: "090c169 verified live at 1000 px (labels read as words, Spending unchanged, Sources ✓ 52,729,370); dates then split at their hyphens, fixed in 805f195 on main, parked on its deploy to verify"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved: 090c169 verified live, 805f195 (nowrap dates, .spend-date min-width auto) pushed to main; the parked continuation verifies it on deploy. No new work."
decidedBy: "ag_s1r27j0txp"
decidedAt: "2026-10-29T01:28:35.526Z"
sessionId: "se_zizveepu09"
assignmentId: "as_v2adg8ct04"
costUsd: 2.9185523999999994
tokens: 58371
turns: 38
createdAt: "2026-10-29T01:28:18.531Z"
updatedAt: "2026-10-29T01:28:35.526Z"
---
## What I did
- Confirmed 090c169 live (GET /api/health commit 090c169 at 00:52Z) and ran a playwright check of https://muster.town/workshop/?guest#/finance at a 1000 px viewport (Sources panel 327 px wide), measuring the DOM and taking section screenshots.
- Found one leftover in the same rows, previewed a fix on the live DOM (addStyleTag + rewriting the spans, measuring widths), applied it in code, ran `npm run typecheck` and the web finance tests (14 passed), pushed 805f195 to main (rebased on d92ef20; no PR, building rule). CI promotes it on its own.

## Findings
- 090c169 did what it said: the third input's label ("Mitchell's Claude subscription (Max 5x): ~80% of the weekly plan…") is 159 px wide and 7 lines of whole words, not one character per line. Spending rows are unchanged (no date column there). The Sources check line reads "✓ Adds up: credited 48,099,993 + donated 4,629,377 = 52,729,370, the Tokens section's total"; Total received 52,729,370 equals the Tokens total.
- Not quite as the assignment expected: the date range did not wrap after the arrow. The `.spend-share` column has min-width 48 px, so beside a long label it shrank to 48 px and split each date at its hyphens ("2026-" / "10-21" / "→" / "2026-" / "10-26"); single dates ("2026-10-20") and the donation dates split the same way, at 1400 px too. No CSS stops a break at a hyphen except nowrap, so 805f195 wraps each date in a nowrap span, gives the Sources date column (`.spend-date`) min-width auto, and puts the arrow with the first date ("2026-10-21 →" / "2026-10-26"). Previewed live at 1000 px: dates whole (73 px, or 87 px for a range on 2 lines), labels 120–134 px and still words (12 lines at most for the longest label); at 1400 px labels 260–274 px. Changed files: packages/web/src/panels/FinancePanel.tsx, styles.css, test/finance.test.tsx (the literal-range assertion now matches the spans).
- Nothing regressed, so 090c169 stays. One side note: the GitHub repo now reports it moved to mitchellgordon95/muster-town; the old remote still redirects.

## What I need from you
Nothing needed. Parked on deploy 805f195 to confirm the date column live.
