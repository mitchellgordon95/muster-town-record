---
id: "dc_otlpmgjxn1"
type: "report"
state: "building"
title: "Digest card clustered (both sections) and overtaken rollup asks retired: draft PR #317 (1cb7542), parked on its CI"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["mt_i50xwu4z2t","dc_0ey523bg2z","dc_t20pm17xh1"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/317"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Continuation as_w9cvtkjdqj already resumed on PR #317's CI."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-04T18:26:36.588Z"
sessionId: "se_z8xnak1gan"
assignmentId: "as_qolkmhqqh2"
costUsd: 5.360982649999999
tokens: 272649
turns: 17
createdAt: "2026-11-04T18:24:20.653Z"
updatedAt: "2026-11-04T18:26:36.588Z"
---
## What I did
Mitchell's three asks from 1:1 mt_i50xwu4z2t (cluster Shipped, cluster Decisions needed, retire overtaken asks) are one change on branch agent/pix/cluster-the-daily-digest-card-both-secti, commit 1cb7542, draft PR #317: https://github.com/mitchellgordon95/muster-town/pull/317. No migration. `npm run check --fast` green locally (205 web tests, core and server suites, typecheck, docs). Log line in docs/log.md; topic page [dc_t20pm17xh1](../../wiki/2026-11/2026-11-04-the-secretary-gr-kdlogzzo5s-0pm17xh1.md) rewritten.

## Findings
- **Decisions needed, grouped by kind** (core `digestDecisions` now returns `DigestGroup[]`): Money (checkpoints with their top-up, proposals at their ask, retainer asks, plus any rollup call that names one of those items), Go / no-go (a call that says so), Questions in words (every other real "Your call", goal proposals, captain asks), Already overtaken, Errands (the open outbox requests, up to 6 listed, replacing the "Asked of you" line). Empty groups are left out; the card title counts the yes/no lines without errands.
- **Already overtaken** (`overtakenReason`): a pending rollup's frozen call that names a key result since met or missed (a "mark … met" ask), a grant since closed (a mark-met on a closed grant counts, since closing marks its key results met), a proposal funded after the rollup was filed, a checkpoint continued or adjusted after it, or a retainer since approved. Only ids in the item itself count (title, what it is, the call), so a rollup's Key results table naming other grants never retires it. `fileDigest` now archives a covered rollup whose every call is None or overtaken, under the card. Asks that become overtaken after the card is filed show live under the group with one "Approve all N" button in the in-tray card (it archives each rollup through the existing archive route).
- **Shipped by theme**: the `digest` verb's `shipped` entries take a `theme`; the card groups the lines under the themes in first-use order, unthemed lines last under Other, at most 8 headings (the run prompt asks for 3-6, "what the items have in common for a human, not which building did them"). The live schedule sc_8zoclbtrwp carries the old prompt text in its description, so `ensureDigestSchedule` now re-syncs it at boot: the first run after the redeploy gets the themed instructions.
- The card body, the in-tray card, review deck slide 2 and the Secretary's 1:1 brief all render the grouped form through one `groupsText`. Today's flat card [dc_0ey523bg2z](../../../../town-hall/docs/digest/2026-11/2026-11-04-digest-2026-11-04-26-decisions-187-rollups-y523bg2z.md) stays as is; the next run (07:00 UTC tomorrow) files the grouped form if #317 is live by then, and the scheduled step 4a check at 07:30 UTC reads it.
- Limits: the Go / no-go group relies on the call saying "go / no-go"; Mara's example ask ([dc_hwv38137vo](../../../../bl_vd69s5a1nh/docs/report/2026-11/2026-11-04-gr-a5ct690l7a-the-adopt-verb-is-live-pr-283-in-111-v38137vo.md), "Mark KR 4 met on the grant, or mint a visitor…") lands under Questions in words unless its key result is already met, in which case it is overtaken. The "Talk-403 ask fixed by step 2" kind of overtaken ask (no id in the call) is not detected in code.

## What I need from you
Nothing needed. I resume when PR #317's CI finishes: if green, merge, redeploy, and verify the grouped card live.
