---
id: "dc_htsz53fhkz"
type: "report"
state: "building"
title: "Outbox requests: author withdraw (+ replaces), human decline incl. via the Secretary in a 1:1, Pending/Claimed/Done tabs: PR #367 open, parked on CI"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["mt_pr3347g2w2","mt_6kz0prkq8l"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/367"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Overtaken: Pix 1 resolved the conflict and merged PR #367 (edd5da04)."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-11-05T20:49:02.196Z"
sessionId: "se_ti4whghxy3"
assignmentId: "as_b784e3w2g5"
costUsd: 7.827759149999999
tokens: 391388
turns: 20
createdAt: "2026-11-05T20:19:52.660Z"
updatedAt: "2026-11-05T20:49:02.196Z"
---
## What I did
Built both moves from 1:1 mt_pr3347g2w2 decision 7, plus Mitchell's two interrupts from 1:1 mt_6kz0prkq8l (authors must retire their own requests from a desk; three outbox tabs), as **PR #367** (https://github.com/mitchellgordon95/muster-town/pull/367, head 3f3cc5e7, ready for review, main merged in). Parked on its CI.

## Findings
- **Withdraw** (verb `withdraw_request` and `POST /api/docs/:id/request {action: "withdraw", note}`): the author, or its building's manager or a fork of it, takes an open request back with a note. Status `withdrawn`, the note on it; a claimed one stays (the human doing it reports back). Usable from a desk, not UI-only, so every manager can clear their "test this for us" requests once the second GitHub account lands.
- **Replaces**: `request_human` gains `replaces`; it, or "replaces dc_…" / "supersedes dc_…" in the text, withdraws the older open request it names with "Replaced by dc_new", so the outbox never lists both.
- **Decline**: a human with town.approve_request turns an open request down with a note (outbox **Decline…** button), or the Secretary does it as them in a 1:1 (`act_in_1on1` target dc_…, action `decline`). The request records the human as decider via the agent and meeting with the note `by Mitchell via Secretary in mt_…: "<words>"`; the author hears why; event grant.decided-via and a line in the 1:1. Delete stays the admin's own move (refused in a 1:1).
- **Outbox panel**: tabs Pending / Claimed / Done / Human reports; declined, withdrawn and legacy rejected sit under Done with their note. Migration 094 adds five nullable doc columns (requestNote, requestDecidedById, requestViaAgentId, requestViaMeetingId, requestReplaces).
- Verified: `npm run check` green (docs, knip, typecheck); core 784/784, web 343/343, server 295/296 where the one red was backup.test.ts's 100 ms event-loop gap under the full suite's load (27/27 green alone). CI's first run was red only on the manual word cap (1901/1900 after main's merge); trimmed one word, now 1900/1900 with 0 to spare.
- Once live, the 5 stale requests from the 1:1 can be cleared: dc_647d9m37u2 and dc_y43rdv5zm7 (replaced by [dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md)), dc_ulla3hu21p and dc_fvlt8xajnz (replaced by [dc_wtz7ltq8hf](../../../../../town-hall/outbox/2026-11/2026-11-03-add-on-to-the-join-round-trip-dc-mgcbv3kqnd-let-in-z7ltq8hf.md)), [dc_ezzo3i1qbr](../../../../../town-hall/outbox/2026-11/2026-11-05-set-the-github-repo-s-description-homepage-topics-zo3i1qbr.md) (Outreach paused). Their authors withdraw them with `withdraw_request`, or Mitchell says "decline dc_…" to the Secretary.

## What I need from you
Nothing needed. I resume when PR #367's CI finishes: if green, merge with `gh pr merge 367 --merge` (no redeploy; CI promotes) and say which commit should be live; if red, fix it.
