---
id: "dc_vk0rkshrou"
type: "report"
state: "building"
title: "Phone outline for the goal tree: PR #509, parked on CI"
authorId: "ag_tyyyjp31qq"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Settled by the town: parked: it resumes by itself."
decidedBy: "system"
decidedAt: "2026-11-19T15:35:40.705Z"
sessionId: "se_obh9ombilu"
assignmentId: "as_nb79jbe06a"
costUsd: 1.6432814999999998
tokens: 82164
turns: 42
createdAt: "2026-11-19T15:35:40.692Z"
updatedAt: "2026-11-19T15:35:40.705Z"
---
## What I did
Built the phone outline view for the goal tree and opened draft PR #509 (commit 497c143f). Checked it on the mock at 390×844 (touch).

## Findings
- PR: https://github.com/mitchellgordon95/muster-town/pull/509
- Below 760 px the goal tree now opens on an outline (new file GoalOutline.tsx). Each goal is one indented row: its words at 13 px, then "Captain X · N key results · N proposals".
- Tapping a row selects the goal and opens its detail in the lower part of the screen.
- An "Outline | Map" toggle switches to the canvas. The choice is saved in localStorage under `musterTown.goalEditor.phoneView`. Desktop has no toggle and does not change.
- Accessibility: the list is role=tree with aria-level and aria-selected. It is one tab stop, and ↑ ↓ Home End move between rows.
- `useNarrow` moved from MeetingSlide.tsx to panelResize.tsx so both files share it.
- Mock check at 390×844: 9 rows, all at 13 px and none clipped. Tapping the third row showed that goal's detail. Map showed the canvas and saved "map".
- Tests: goalTree.test.tsx has 3 new tests. All 445 web tests pass, and typecheck passes. CI is still running.
- Topic page [dc_7z5fhlkrq7](../../wiki/2026-11/2026-11-19-goal-tree-readable-at-first-look-gr-nhayb7s9bd-5fhlkrq7.md) is updated, including the plan for step 3.

## What I need from you
Nothing needed.
