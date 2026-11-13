---
id: "dc_3aaga3xa4x"
type: "report"
state: "building"
title: "Weekly check-timing watch: no slowdown (last 12 green main runs)"
authorId: "ag_0mfjf3xblq"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Weekly watch read: no slowdown, total median 133 s (8 s under the 141 s threshold), tests median 105 s since PR #434. The one-shot sc_owiul5muej reads the 10th run for kr_0xk1ex7tus on 11-14 02:00Z. Nothing to queue."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-13T06:01:41.662Z"
sessionId: "se_e347obod7p"
assignmentId: "as_h7z830rj5c"
costUsd: 0.02364989
tokens: 1182
turns: 8
createdAt: "2026-11-13T06:01:24.928Z"
updatedAt: "2026-11-13T06:01:41.662Z"
---
## What I did
Read the last 12 green push runs of ci.yml on main (15:24Z to 23:02Z on 2026-11-12). Pulled each `check:` line from the check job log and GitHub's job duration. Rewrote the "Build times / fast check" topic page ([dc_87kealnkye](../../wiki/2026-10/2026-10-29-build-times-fast-check-kealnkye.md)) with this week's numbers. No code changes, no PR.

## Findings
No slowdown. The history page stays unproposed.

Check-line medians over the 12 runs (ranges in brackets):

| Step | Median | Range | Baseline / last reading | Verdict |
|---|---|---|---|---|
| total | 133 s | 93–211 s | 94 s (10-30); 180 s (11-06) | below 141 s threshold |
| tests | 107.5 s | 76–182 s | 76.5 s (10-30); 158 s (11-06) | under 2× baseline |
| typecheck | 20.5 s | 12–25 s | tracks runner variance | normal |
| deadcode | 5.5 s | 3–7 s | — | normal |
| docs | ≤1 s | 0–1 s | — | normal |
| GitHub job duration | 153 s | 110–235 s | no baseline on the page yet | ~25–35 s over check total (checkout, install) |

- **Runs over 180 s:** two sit in the window, both before PR #434 (aa2674b5): 43249296567 (check total 211 s, job 235 s) and 43256828667 (check total 166 s). None since aa2674b5 is over 147 s check total.
- **Since #434 (9 runs from aa2674b5):** tests median 105 s (76–116 s), total median 133 s (93–147 s). Kr_0xk1ex7tus needs a 10th run, which the one-shot sc_owiul5muej reads 2026-11-14 02:00Z.
- **Margin:** the total median is about 8 s under the 141 s threshold, so it is close. Watch it next week.

## What I need from you
Nothing needed.

Verdict: stop (no slowdown this week).
