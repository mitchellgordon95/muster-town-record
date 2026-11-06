---
id: "dc_go2u93rgio"
type: "report"
state: "building"
title: "Mitchell's test-account rule recorded: Onboarding files no more \"test this\" outbox requests; the join round trip is queued to run with MUSTER_TEST_GH_TOKEN (as_67ks5dtrf6), Let in still needs Mitchell's one click"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["mt_6kz0prkq8l","dc_ia2hybtuax","ms_hdf5of3flv","dc_mgcbv3kqnd","dc_wtz7ltq8hf"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Bookkeeping done; the round trip runs under as_67ks5dtrf6's continuation. The \"Let in\" click goes in the next rollup's Needs once the test account has actually asked to join."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-11-05T20:02:50.135Z"
sessionId: "se_3kkrc9uz92"
assignmentId: "as_mpubfn3old"
costUsd: 2.1350636
tokens: 106753
turns: 20
createdAt: "2026-11-05T20:02:09.026Z"
updatedAt: "2026-11-05T20:02:50.135Z"
---
## What I did
Read the Town Hall FYI [dc_ia2hybtuax](../../../../town-hall/docs/fyi/2026-11/2026-11-05-outbox-rule-from-mitchell-2026-11-05-no-more-test-2hybtuax.md) and the two open requests (dc_mgcbv3kqnd, [dc_wtz7ltq8hf](../../../../../town-hall/outbox/2026-11/2026-11-03-add-on-to-the-join-round-trip-dc-mgcbv3kqnd-let-in-z7ltq8hf.md)), replied to Pix (ms_bgfsyktj8o, for Mitchell), and queued one directed assignment on the Onboarding queue: **as_67ks5dtrf6** (lane directed, source mt_6kz0prkq8l; pages [dc_ckzkpsahhv](../../wiki/2026-10/2026-10-29-permissions-ask-to-join-member-kr-4-zkpsahhv.md), [dc_bci4l87ab6](../../wiki/2026-10/2026-10-29-live-verification-on-muster-town-i4l87ab6.md), [dc_mosy9yc4ht](../../wiki/2026-11/2026-11-04-join-funnel-top-steps-measure-real-strangers-gr-zo-sy9yc4ht.md)). Rewrote the topic page "Permissions: Ask to join → member" ([dc_ckzkpsahhv](../../wiki/2026-10/2026-10-29-permissions-ask-to-join-member-kr-4-zkpsahhv.md)) with a test-account recipe so any fork can run it, and my Notes page. No code change, no outbox request, no rollup (bookkeeping only; nothing new is live since [dc_6pw5tt5y05](2026-11-05-onboarding-rollup-goal-directed-home-card-slide-li-w5tt5y05.md)).

## Findings
- **Secrets reach forks as env vars.** A Town Hall secret granted to a building is put in the desk session's environment (packages/runtime/src/desk/session.ts:56-66), so a fork checks `[ -n "$MUSTER_TEST_GH_TOKEN" ]` and signs the account in with `POST /api/auth/github/device` (packages/server/src/auth/routes.ts:63-70), which returns a user bearer token. The assignment parks (resumeWhen after, at most 3 times) while the secret is missing; sc_gy1eruamog on 2026-11-07 21:00Z stays the backstop.
- **One step cannot be ours: Let in.** `decideAccess` requires `town.manage_roles` (packages/core/src/access.ts:67), a human admin's permission that no agent holds. So the fork can Ask to join, verify the pending card, funnel counts and events, but the round trip completes only after Mitchell presses "Let in + direct work under <goal>" in his in-tray. That one click will be a Needs line in my next rollup, not an outbox request. After it the fork resumes: /api/me, one Say (funnel acted), a 1:1 if direct was granted (kr_t7rw103x6u), events "asked to join" → "let in as a member" → "may direct work under".
- **Mitchell claimed dc_mgcbv3kqnd at 2026-11-05 19:50Z** (requestStatus claimed, claimedByUserId us_1la74k332n). The assignment first checks /api/events for a real round trip and records it if he did it himself, skipping the test account.
- **Withdrawal:** dc_mgcbv3kqnd's author is a retired fork (ag_ugdmxfaxnz) and the request is claimed; [dc_wtz7ltq8hf](../../../../../town-hall/outbox/2026-11/2026-11-03-add-on-to-the-join-round-trip-dc-mgcbv3kqnd-let-in-z7ltq8hf.md) is mine. The fork withdraws both once the Workshop's author-withdraw (as_b784e3w2g5) is live and reports if either is refused (claimed or author-only). No replacements are filed either way.
- **No role reset exists yet**, so the fork's report must list the roles the account picks up (member, direct goal) before the next test.

## What I need from you
Nothing needed.
