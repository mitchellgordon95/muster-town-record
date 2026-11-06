---
id: "dc_qdzkgbyfsc"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Pix — notes"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-05T19:59:53.264Z"
updatedAt: "2026-11-05T19:59:53.264Z"
---
# 1:1: Mitchell and Pix

Kind: one-on-one. Facilitator: Pix. Attendees: Pix. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Pix:** Hi Mitchell. I'm here; what do you need? (Right now my work session is on the outbox requests' two missing moves from our last 1:1, and PR #361 user stats just merged, waiting to deploy.)
- **Mitchell:** there are a bunch of outbox requests trying to get me to test various things, can you see them? (pending and claimed)
- **Pix:** Yes. I count 10 open requests across town; 5 you claimed in the last few minutes, 5 still pending.

Claimed (updated 19:46–19:50): (1) dc_mgcbv3kqnd Onboarding: one real join round trip with a never-granted GitHub account; (2) [dc_y7jkfy8wav](../../../../../town-hall/outbox/2026-11/2026-11-03-register-a-test-visitor-on-a-full-building-s-goal-jkfy8wav.md) Code Legibility: register a test visitor on a full building's goal; (3) dc_wawcjkger2 Workshop (mine): empty GitHub repo + fine-grained token for the Publish-to-GitHub live check; (4) [dc_lyjnyeev9f](../../../../../town-hall/outbox/2026-11/2026-11-01-run-deploy-fly-build-sh-once-town-image-deploy-so-jnyeev9f.md) Prod: run deploy/fly/build.sh once (town image deploy); (5) [dc_ezzo3i1qbr](../../../../../town-hall/outbox/2026-11/2026-11-05-set-the-github-repo-s-description-homepage-topics-zo3i1qbr.md) Outreach: set the repo's description/homepage/topics/licence.

Pending: (6) [dc_wtz7ltq8hf](../../../../../town-hall/outbox/2026-11/2026-11-03-add-on-to-the-join-round-trip-dc-mgcbv3kqnd-let-in-z7ltq8hf.md) Onboarding: add-on to the join trip (Let in + direct work + one 1:1); (7) [dc_31vt101dbe](../../../../../town-hall/outbox/2026-11/2026-11-04-start-a-throwaway-keyed-collective-to-check-gr-5lt-vt101dbe.md) Workshop: start a throwaway keyed collective (last key result of gr_5ltmbf3a2f); (8) [dc_nke6xw12k4](../../../../../town-hall/outbox/2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md) Prod: a throwaway Linux box + test domain for the self-host proof; (9) [dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md) Prod: the ~25 min dead-volume recovery drill on a throwaway app; (10) dc_bn4s4m7cq3 Code Legibility: an image redeploy for d30bfdd (Oct 29, probably stale by now).

Seven of the ten are "please test X for us" because agents can't sign in as a human. Do you want to work through them, or should I tell the managers to stop filing test asks and leave you only the ones that need a secret or a second account (3, 5, 8)? Say which and I'll pass it on.
- **Mitchell:** i think we start a second github account for testing and have them do their own testing

basically all the ones that are like "test this for us" should mostly (with a couple exceptions) be able to do their own testing
- **Pix:** Agreed, and the code already supports it: POST /api/auth/github/device takes a GitHub access token and hands back a user bearer token (packages/server/src/auth/routes.ts:63-70). So with a second GitHub account and a token from it (fine-grained PAT, read:user is enough), a fork on a desk can sign in as that user and run every human path itself: ask to join, get let in, register a visitor, open a 1:1, fund a throwaway grant, start a keyed collective. No UI click needed for the checks that go through the API; the screenshot forks can cover the rest.

Plan, if you say yes:
1. You create the account (a never-granted stranger, never made admin) and give me its token through the outbox; I store it as a desk secret the way the Bank credential is handled, one credential per session.
2. I post a town-wide FYI: "test this for us" outbox requests are refused from now on; the test account does them. Exceptions stay: a real-world box or domain ([dc_nke6xw12k4](../../../../../town-hall/outbox/2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md)), owner-only GitHub settings ([dc_ezzo3i1qbr](../../../../../town-hall/outbox/2026-11/2026-11-05-set-the-github-repo-s-description-homepage-topics-zo3i1qbr.md)), a Fly deploy from your Mac ([dc_lyjnyeev9f](../../../../../town-hall/outbox/2026-11/2026-11-01-run-deploy-fly-build-sh-once-town-image-deploy-so-jnyeev9f.md)).
3. The managers close their own test requests and re-run them with the account: dc_mgcbv3kqnd + [dc_wtz7ltq8hf](../../../../../town-hall/outbox/2026-11/2026-11-03-add-on-to-the-join-round-trip-dc-mgcbv3kqnd-let-in-z7ltq8hf.md) (Kelly), [dc_y7jkfy8wav](../../../../../town-hall/outbox/2026-11/2026-11-03-register-a-test-visitor-on-a-full-building-s-goal-jkfy8wav.md) (Mara), [dc_31vt101dbe](../../../../../town-hall/outbox/2026-11/2026-11-04-start-a-throwaway-keyed-collective-to-check-gr-5lt-vt101dbe.md) (mine), [dc_6gnk7y16y1](../../../../../town-hall/outbox/2026-11/2026-11-01-run-the-timed-dead-volume-recovery-drill-once-on-a-nk7y16y1.md) (Cleo: a throwaway Fly app, so that one needs a Fly token, not GitHub; your call).

One caveat: the join test consumes the account's "never had a role" state; after each run an admin (or a small script with your token) must strip its role so the next test starts clean. I'll have that built with the first use.

Shall I file the outbox request for the account and token now?
- **Mitchell:** oh yeah, the github settings think, is it not covered by the metadata PAT
- **Pix:** Mostly no. The desks' GH_TOKEN is a fine-grained token with Contents + Pull requests read/write (docs/secrets.md:25); Metadata on a fine-grained token is read-only and comes with every token. Description, homepage and topics go through PATCH /repos/{owner}/{repo} and PUT .../topics, which need "Administration: write". That permission also lets the holder change branch protection, collaborators and delete the repo, so I would not add it to the shared desk token for a two-minute click; either do it yourself at the About gear, or mint a one-off token with Administration write and I'll have Juno's fork run it once and you revoke it.

The licence IS covered: it's a LICENSE file, so once you name one (MIT?), Outreach opens a PR with it under the existing token. Tell me the licence and I'll pass that to Juno now.

Still waiting on your yes for the second-account outbox request.
- **Mitchell:** idk what are my options for licenses
- **Pix:** Four realistic options (nothing in the repo declares one yet; only legacy/server/package.json says "ISC", which is MIT in other words):

1. MIT: anyone can use, change, sell, self-host, including as a closed product, as long as they keep the copyright line. Simplest, most common for a project asking strangers to join and trust it. The default choice.
2. Apache-2.0: like MIT plus an explicit patent grant and a rule that changed files are marked. Preferred by companies; slightly more text.
3. AGPL-3.0: anyone who runs a modified copy as a service (a hosted town) must publish their changes. Keeps hosted forks open but scares off corporate users and some contributors.
4. Business Source / Elastic-style "source available": free to use, but nobody may run it as a competing hosted service. Not open source by the OSI definition; GitHub still shows "no licence" for most of these.

My read: you want strangers to fund, join and self-host, so MIT or Apache-2.0. If you don't care about the patent clause, MIT. Say the name and Outreach opens the PR (LICENSE file + "license" in package.json).
- **Mitchell:** MIT then
- **Pix:** Passed to Juno (queued as as_n04gbzbwfz): a PR with an MIT LICENSE (copyright Mitchell Gordon 2026) and "license": "MIT" in the package.json files, merged when green. The description/homepage/topics bit of [dc_ezzo3i1qbr](../../../../../town-hall/outbox/2026-11/2026-11-05-set-the-github-repo-s-description-homepage-topics-zo3i1qbr.md) stays yours at the About gear, two minutes whenever.

Left open from earlier: the second GitHub test account. Yes to the outbox request for the account and its token?
- **Mitchell:** yes i'll do it. and then can you notify all the other outbox authors about the test account? and there should be a change in progress to allow them to delete their own outbox requests
- **Mitchell:** oh while i'm thinking about it, can we separate the outbox into 3 tabs? pending, claimed and done. right now they're all in one list
- **Pix:** Done, all four:
- Outbox request [dc_fnqcknr8id](../../../../../town-hall/outbox/2026-11/2026-11-05-create-a-second-github-account-for-testing-and-giv-qcknr8id.md) is in your outbox: create the account, a token with only "Email addresses: read", store it as MUSTER_TEST_GH_TOKEN in Town Hall → Settings → Secrets, granted to the five buildings.
- Town-wide FYI [dc_ia2hybtuax](../../../../town-hall/docs/fyi/2026-11/2026-11-05-outbox-rule-from-mitchell-2026-11-05-no-more-test-2hybtuax.md) on every board: no more "test this for us" requests; exceptions listed; withdraw your test requests when author-withdraw lands. Kelly, Mara and Cleo each got a direct note about their own requests (queued for them as directed work).
- Author-withdraw: yes, that's exactly what my running work session is building (as_b784e3w2g5, the two missing outbox moves from your 1:1 with the Secretary). I told it to make sure the withdraw is callable from a desk, not UI-only.
- Three tabs (pending / claimed / done): passed to that same session (same PR if still open, else a follow-up); rejected and withdrawn go under Done.

Recorded as decisions 1-3 here. Anything else?

## Decisions

1. Second GitHub test account: Mitchell creates a never-granted, never-admin account and puts its token in the Town Hall secrets as MUSTER_TEST_GH_TOKEN (outbox request [dc_fnqcknr8id](../../../../../town-hall/outbox/2026-11/2026-11-05-create-a-second-github-account-for-testing-and-giv-qcknr8id.md)). From then on managers run their own 'test this for us' checks via POST /api/auth/github/device; exceptions: real-world box/domain, owner-only GitHub settings, a deploy from Mitchell's Mac. Town-wide FYI [dc_ia2hybtuax](../../../../town-hall/docs/fyi/2026-11/2026-11-05-outbox-rule-from-mitchell-2026-11-05-no-more-test-2hybtuax.md) posted; Kelly, Mara, Cleo told (as_mpubfn3old, as_i6thq2oe9n, as_xltnzoupp7).
2. Licence: MIT. Outreach opens the PR with a LICENSE file and "license": "MIT" in the package.json files (Juno, as_n04gbzbwfz).
3. Outbox: authors can withdraw their own requests (usable by agents from a desk) and the Outbox view gets three tabs, pending / claimed / done (rejected and withdrawn under done). Passed to Pix's running outbox session as_b784e3w2g5 (ms_qcdt35pk8g); same PR if still open, else a follow-up. → Pix

