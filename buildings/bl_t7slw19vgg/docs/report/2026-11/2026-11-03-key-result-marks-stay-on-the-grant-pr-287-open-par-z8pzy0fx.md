---
id: "dc_zgz8pzy0fx"
type: "report"
state: "building"
title: "Key-result marks stay on the grant: PR #287 open, parked on CI"
authorId: "ag_slnb9eecsi"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Fix for Mitchell's flag dc_nm5lwzye7a is on PR #287; the continuation as_w5444ozlxm already waits on its CI to merge and redeploy. Nothing more to queue."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-03T23:08:56.671Z"
sessionId: "se_9m6e63pc7f"
assignmentId: "as_71qbtmbexd"
costUsd: 1.2219477000000003
tokens: 61097
turns: 36
createdAt: "2026-11-03T23:08:46.758Z"
updatedAt: "2026-11-03T23:08:56.671Z"
---
## What I did
I fixed Mitchell's flag [dc_nm5lwzye7a](../../flag/2026-11/2026-11-03-clicking-key-result-met-or-missed-takes-me-back-to-5lwzye7a.md): marking a key result met or missed no longer sends him back to the in-tray overview. PR https://github.com/mitchellgordon95/muster-town/pull/287 (draft, commit on branch `agent/teo-1/mitchell-s-flag-clicking-key-result-met-`). I'm parked on its CI; when it passes I merge it and redeploy.

## Findings
- **Cause:** `GrantRow`'s `mark` called `onDecided`. In the in-tray focus view (`Places.tsx:82`) that runs `setFocus(null)`. In the review deck it jumps to the next slide.
- **Fix:** `GrantRow` now takes `onMarked`, which defaults to `onDecided`.
  - In the in-tray focus view it passes `list.reload`, so the same grant re-renders with the new status on its line. Once no key result is still claimed, the server (core `domain.ts:355`) drops the grant from the in-tray and the overview shows.
  - In the deck a mark reloads and stays on the same slide. If that grant left the deck, the same position now holds the next item.
  - Fund, counter, reject, continue, cut, close and stop are unchanged. DocView has no key-result buttons, so it needed no change.
- **Mock fixes needed for the check:**
  - The mock in-tray waited only on the grant's first key result; core waits on any claimed one. The mock now matches core.
  - Marking a key result in the mock now updates the grant's `keyResults`.
  - Mock grant gr_stress now carries two claimed key results.
- **Verified** in the mock town (headless Chromium at 1280×900):
  - After the first mark the grant stays open. Key result 1 reads "· met" and key result 2 is still "claimed", with its buttons.
  - After the second mark the in-tray overview shows.
  - `npm run typecheck` and the web tests pass (286).
  - The deck path is checked only by reading the code, not in the browser.

## What I need from you
Nothing needed.
