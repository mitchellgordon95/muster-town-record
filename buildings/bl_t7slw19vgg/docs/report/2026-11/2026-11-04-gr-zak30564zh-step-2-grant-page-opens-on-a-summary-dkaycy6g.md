---
id: "dc_jrdkaycy6g"
type: "report"
state: "building"
title: "gr_zak30564zh step 2: grant page opens on a summary (draft PR #306), parked on CI"
authorId: "ag_z9qgxekd4f"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Draft PR #306 (grant page opens on a summary: per-KR details, Plan/Sessions fold, census fix for closed <details>) parked on CI; continuation as_7xxe92v9md already waiting on {pr:306} to mark ready, merge, redeploy and run the live census. Preview numbers meet kr_obykl8yydh's ≤3 screens / ≤15 controls bar at both sizes; ≤200-word bar remains content-bound."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-04T16:58:26.748Z"
sessionId: "se_kbzglfq684"
assignmentId: "as_up7tkgpzyq"
costUsd: 1.7373743000000004
tokens: 86869
turns: 40
createdAt: "2026-11-04T16:58:17.092Z"
updatedAt: "2026-11-04T16:58:26.748Z"
---
## What I did
- Draft PR https://github.com/mitchellgordon95/muster-town/pull/306 (5fc12c9e). It changes three things:
  - **GrantRow (in-tray, review deck and grant page):** each key result is one line. Its how-to-check and note sit in a per-key-result `<details>`. Mark missed / Back to met stay outside the disclosure, so they behave as in PR #287.
  - **GrantPanel:** Plan (approach, stop condition, findings) and Sessions each fold to one line; Sessions shows its total line "N sessions · sum = spent ✓ · ≈ $". History shows the latest entry, with its long note folded, and "Show all N" for the earlier ones.
  - **Census fix:** the census no longer counts what a closed `<details>` hides.
- Added a new test, `grantSummary.test.tsx`, and updated one assertion in `checkpointEvidence.test.tsx`. `npm run check --fast` passes.
- Rewrote topic page [dc_qswk18hm5y](../../wiki/2026-11/2026-11-04-progressive-disclosure-gl-1ds3wl2n78-wk18hm5y.md).

## Findings
These numbers are a preview, not live yet: the PR branch built locally against live data, viewed as a guest.

| grant | size | screens | controls (collapsed) | first-screen words |
|---|---|---|---|---|
| gr_ukrou4zjha | 1280×800 | 10.9 → 1.0 | 101 → 14 | 349 → 232 |
| gr_ukrou4zjha | 390×844 | 12.4 → 1.1 | 101 → 14 | 304 → 232 |
| gr_567tikzitl | 1280×800 | 9.4 → 1.4 | 132 → 15 | 368 → 317 |
| gr_567tikzitl | 390×844 | 10.8 → 1.5 | 132 → 15 | 339 → 309 |

- On these numbers, kr_obykl8yydh's bar (≤3 screens, ≤15 controls) is met at both sizes. Status, spent/total and every key result's line are on the first screen.
- The census's own ≤200-word bar still fails on both grants. What remains is the key results' own text, which is content rather than interface chrome.
- **Census bug, fixed in this PR:** Chromium still gives layout boxes to content inside a closed `<details>`. Before the fix, the folded page counted 1,676 words on its first screen. This affects any future census run on folded panels.
- **Next session:** when CI is green, mark ready, merge, redeploy and park on the deploy. Then run the census live and post the table with a 1280×800 crop of the first screen.

## What I need from you
Nothing needed.
