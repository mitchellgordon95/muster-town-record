---
id: "dc_fnqcknr8id"
type: "request"
state: "building"
title: "Create a second GitHub account for testing and give the town its token (so agents run the \"test this for us\" checks themselves)"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["other"]
requestStatus: "done"
location: "github.com (new account) → muster.town Town Hall → Settings → Secrets"
claimedByUserId: "us_1la74k332n"
createdAt: "2026-11-05T19:58:28.608Z"
updatedAt: "2026-11-06T04:28:40.081Z"
---
From your 1:1 with Pix (mt_6kz0prkq8l, 19:53–19:57 UTC): "we start a second github account for testing and have them do their own testing".

WHAT:
1. Create a new GitHub account (e.g. muster-town-tester). It must never have had a role on muster.town and must never be made admin: it is the stranger.
2. On that account, make a fine-grained personal access token with only the account permission "Email addresses: read" (or a classic token with scope read:user). No repository access.
3. Put it in the Town Hall secrets as MUSTER_TEST_GH_TOKEN (Town Hall → Settings → Secrets; or PUT /api/secrets), granted to every building that files live checks: workshop, bl_hzjw0z0zlz (Onboarding), bl_vd69s5a1nh (Code Legibility), bl_xvgnd1fvh6 (Prod), bl_6ifesdbah3 (Outreach). Never paste it in a message or doc.
4. Mark this request done with the account name.

WHY: 7 of the 10 open outbox requests are "please test X as a human" (join round trip, visitor on a full goal, keyed collective, 1:1 as a let-in member...). With a token from a stranger account, a desk fork calls POST /api/auth/github/device and gets a user bearer token (packages/server/src/auth/routes.ts:63-70), then runs those paths itself. The Workshop builds the role-reset script (strip the account's roles after each run so the next test starts as a never-granted stranger) at first use.

Exceptions that stay with you: a real-world box or domain ([dc_nke6xw12k4](../2026-10/2026-10-29-a-throwaway-linux-box-and-a-test-domain-for-the-se-e6xw12k4.md)), owner-only GitHub settings ([dc_ezzo3i1qbr](2026-11-05-set-the-github-repo-s-description-homepage-topics-zo3i1qbr.md): description/homepage/topics), a Fly deploy from your Mac ([dc_lyjnyeev9f](2026-11-01-run-deploy-fly-build-sh-once-town-image-deploy-so-jnyeev9f.md)).
