---
id: "dc_gb8f9btiqr"
type: "report"
state: "building"
title: "Retainer Counter on the ask card takes tokens per run, end date and note (PR #410, parked on CI)"
authorId: "ag_oxtvcdixzy"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved: retainer Counter form (tokens per run, end date, note) in draft PR #410, the last part of Mitchell's mt_ewxnhs90cq decision 3. Continuation as_fvy0j0ohkk already waits on {pr: 410} to merge if green and park on deploy; nothing more to queue. No rollup yet: nothing new live since the last one."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-10T18:13:00.538Z"
sessionId: "se_bmmoit20va"
assignmentId: "as_zpz8oa0ytu"
costUsd: 0.8894932000000001
tokens: 48332
turns: 14
createdAt: "2026-11-10T18:12:53.675Z"
updatedAt: "2026-11-10T18:13:00.538Z"
---
## What I did
Built the only part of decision 3 that was left: the retainer Counter form. Parts (1) and (2), the click-ask notes and the request notes, were already live from PR #408 (57a573df), so I didn't redo them, as Teo said. Draft PR #410 (commit cd45d7d0): https://github.com/mitchellgordon95/muster-town/pull/410

## Findings
- In the decision queue and the review deck, a retainer ask's **Counter…** now opens the same kind of form as a grant's Counter:
  - **Tokens per run**: in M tokens, starting at the amount the schedule asked for.
  - **Ends**: a date, optional.
  - **Note**: optional.
- Counter stays disabled until one of those would change something, because the server refuses an empty counter (core retainers.ts:199).
- What gets sent:
  - The per-run amount only if it differs from the asked one.
  - The end date as the last second of that day, UTC.
  - The server already takes both fields, so there is no server change.
- Code changes:
  - `asks.ts`: the retainer form, and a new `retainerCounter()` helper.
  - `AskCard.tsx`: the form itself. It takes a new optional `retainer` prop.
  - DecisionQueue and ReviewDeck now pass the ask's schedule from the in-tray's retainers.
  - One CSS row.
- Checks: typecheck passes, all 416 web tests pass (2 of them new, in askCard.test.tsx), and the dead-code check (knip) is clean. CI is pending.
- Plan for the next session: when CI finishes, mark #410 ready and squash-merge if green (no redeploy), then park on its deploy. On live, check that the bundle has "Tokens per run" in the ask form. Nobody can test it end to end until a retainer ask is open.

## What I need from you
Nothing needed.
