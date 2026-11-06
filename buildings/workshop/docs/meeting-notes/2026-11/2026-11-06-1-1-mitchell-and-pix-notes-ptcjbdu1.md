---
id: "dc_lzptcjbdu1"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Pix — notes"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-06T04:23:19.693Z"
updatedAt: "2026-11-06T04:23:19.693Z"
---
# 1:1: Mitchell and Pix

Kind: one-on-one. Facilitator: Pix. Attendees: Pix. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Mitchell:** I'd like to talk about the checkpoint grant "A founder's new collective starts working on their goal by itself: their own goal tree with them as captain, a first bu…" (gr_5ltmbf3a2f), for key result kr_n2zh7s6s2s: "A new hosted collective's goal tree is the founder's: root = their goal, founder is captain, no Fund/Join/Trust pillars; Hollyville's empty pillars retired". (presented: Grant: A founder's new collective starts working on their goal by itself: their own goal tree with them as captain, a first building with a resident at a desk, and a first exploration on their key that lands a grant proposal in their in-tray within the first hour. (page grant:gr_5ltmbf3a2f))
- **Pix:** Hi Mitchell. Where kr_n2zh7s6s2s stands: it is done and was checked live. PR #243 (6a541e4) made a hosted collective's seed root = the Start form's goal with the founder as captain and no Fund/Join/Trust pillars (packages/core/src/goals.ts:16 keeps those three only as the Workshop's placeholders; test goals-hosted.test.ts:26). Pix 1 checked Hollyville live on 11-01 as a guest: root "Make money", owner Edward Li, children [] ([dc_t0bx9g9vvh](../../report/2026-11/2026-11-01-hollyville-s-goal-tree-is-now-the-founder-s-243-6a-bx9g9vvh.md)). Since then you retired Hollyville itself (11-05, /hollyville/ → 410), so the "empty pillars retired" half is moot: there is no Hollyville tree to look at any more; the next collective you start shows the same thing.

The grant gr_5ltmbf3a2f as a whole is held at its checkpoint, 648k of 750k spent. KR1 and KR2 (first building + "Add your API key" step) are both claimed with live evidence. Only KR3 (keyed collective explores and a proposal reaches the founder within an hour) is still "on-track": covered by a server test (PR #252), never seen live, because starting a keyed collective needs a GitHub sign-in and a Console key to spend. I withdrew the "test this" outbox request under your rule; it waits on the MUSTER_TEST_GH_TOKEN secret, and a key is still your call.

My suggestion: mark kr_n2zh7s6s2s met now (it is), and either cut the grant with KR3 on test evidence only, or continue it only once the test account is in so a fork can run the keyed check itself. What would you like?

## Decisions

(none)
