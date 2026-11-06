---
id: "mt_okbomo5u3v"
kind: "one-on-one"
buildingId: "workshop"
title: "1:1: Mitchell and Pix"
scheduledAt: "2026-11-06T04:21:53.912Z"
phase: "done"
facilitatorId: "ag_mh0qidzgw6"
attendeeIds: ["ag_mh0qidzgw6"]
agenda: ""
brings: {"mode":"status","text":""}
askHumans: false
deck: null
summaries: {}
transcript: [{"speakerId":"us_1la74k332n","speakerKind":"user","text":"I'd like to talk about the checkpoint grant \"A founder's new collective starts working on their goal by itself: their own goal tree with them as captain, a first bu…\" (gr_5ltmbf3a2f), for key result kr_n2zh7s6s2s: \"A new hosted collective's goal tree is the founder's: root = their goal, founder is captain, no Fund/Join/Trust pillars; Hollyville's empty pillars retired\".","at":"2026-11-06T04:21:53.918Z","attachment":{"kind":"page","ref":"grant:gr_5ltmbf3a2f","title":"Grant: A founder's new collective starts working on their goal by itself: their own goal tree with them as captain, a first building with a resident at a desk, and a first exploration on their key that lands a grant proposal in their in-tray within the first hour."}},{"speakerId":"ag_mh0qidzgw6","speakerKind":"agent","text":"Hi Mitchell. Where kr_n2zh7s6s2s stands: it is done and was checked live. PR #243 (6a541e4) made a hosted collective's seed root = the Start form's goal with the founder as captain and no Fund/Join/Trust pillars (packages/core/src/goals.ts:16 keeps those three only as the Workshop's placeholders; test goals-hosted.test.ts:26). Pix 1 checked Hollyville live on 11-01 as a guest: root \"Make money\", owner Edward Li, children [] (dc_t0bx9g9vvh). Since then you retired Hollyville itself (11-05, /hollyville/ → 410), so the \"empty pillars retired\" half is moot: there is no Hollyville tree to look at any more; the next collective you start shows the same thing.\n\nThe grant gr_5ltmbf3a2f as a whole is held at its checkpoint, 648k of 750k spent. KR1 and KR2 (first building + \"Add your API key\" step) are both claimed with live evidence. Only KR3 (keyed collective explores and a proposal reaches the founder within an hour) is still \"on-track\": covered by a server test (PR #252), never seen live, because starting a keyed collective needs a GitHub sign-in and a Console key to spend. I withdrew the \"test this\" outbox request under your rule; it waits on the MUSTER_TEST_GH_TOKEN secret, and a key is still your call.\n\nMy suggestion: mark kr_n2zh7s6s2s met now (it is), and either cut the grant with KR3 on test evidence only, or continue it only once the test account is in so a fork can run the keyed check itself. What would you like?","at":"2026-11-06T04:22:37.394Z"}]
decisions: []
notesDocId: "dc_lzptcjbdu1"
withUserId: "us_1la74k332n"
createdAt: "2026-11-06T04:21:53.912Z"
startedAt: "2026-11-06T04:21:53.912Z"
endedAt: "2026-11-06T04:23:19.696Z"
---
# 1:1: Mitchell and Pix

- **Mitchell** (2026-11-06T04:21:53.918Z): I'd like to talk about the checkpoint grant "A founder's new collective starts working on their goal by itself: their own goal tree with them as captain, a first bu…" (gr_5ltmbf3a2f), for key result kr_n2zh7s6s2s: "A new hosted collective's goal tree is the founder's: root = their goal, founder is captain, no Fund/Join/Trust pillars; Hollyville's empty pillars retired".
- **Pix** (2026-11-06T04:22:37.394Z): Hi Mitchell. Where kr_n2zh7s6s2s stands: it is done and was checked live. PR #243 (6a541e4) made a hosted collective's seed root = the Start form's goal with the founder as captain and no Fund/Join/Trust pillars (packages/core/src/goals.ts:16 keeps those three only as the Workshop's placeholders; test goals-hosted.test.ts:26). Pix 1 checked Hollyville live on 11-01 as a guest: root "Make money", owner Edward Li, children [] (dc_t0bx9g9vvh). Since then you retired Hollyville itself (11-05, /hollyville/ → 410), so the "empty pillars retired" half is moot: there is no Hollyville tree to look at any more; the next collective you start shows the same thing.

The grant gr_5ltmbf3a2f as a whole is held at its checkpoint, 648k of 750k spent. KR1 and KR2 (first building + "Add your API key" step) are both claimed with live evidence. Only KR3 (keyed collective explores and a proposal reaches the founder within an hour) is still "on-track": covered by a server test (PR #252), never seen live, because starting a keyed collective needs a GitHub sign-in and a Console key to spend. I withdrew the "test this" outbox request under your rule; it waits on the MUSTER_TEST_GH_TOKEN secret, and a key is still your call.

My suggestion: mark kr_n2zh7s6s2s met now (it is), and either cut the grant with KR3 on test evidence only, or continue it only once the test account is in so a fork can run the keyed check itself. What would you like?
