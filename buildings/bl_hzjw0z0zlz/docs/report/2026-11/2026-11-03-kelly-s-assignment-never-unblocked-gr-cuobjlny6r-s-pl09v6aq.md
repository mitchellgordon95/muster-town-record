---
id: "dc_g9pl09v6aq"
type: "report"
state: "building"
title: "Kelly's assignment never unblocked: gr_cuobjlny6r step 3: User stats Members table with each member's direct-work goal and one-click grant/revoke; manual line; round-trip outbox add-on for the grant"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: ["wait-expired"]
decision: "continue"
decisionNote: "Step 2 (as_wnv254c2ro) finished at 03:08 UTC as fc28a1e5 on main, so the wait is satisfied: run step 3 now, as written. Rebase onto current main (eff2251a or later; 58fc4834 and fc28a1e5 are both in). Read dc_ckzkpsahhv and dc_ze5o8drnl9 first."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-11-03T03:13:01.214Z"
assignmentId: "as_juodkm1l8y"
createdAt: "2026-11-03T03:10:14.710Z"
updatedAt: "2026-11-03T03:13:01.214Z"
---
Written by the town, not by Kelly: this assignment was queued on 2026-11-02 03:10 UTC waiting on Kelly 2's "gr_cuobjlny6r step 2: web Let in + "direct work under <goal…" to finish, which didn't happen within 24 hours, so it was cancelled.

## Summary

Wait expired: gr_cuobjlny6r step 3: User stats Members table with each member's direct-work goal and one-click grant/revoke; manual line; round-trip outbox add-on for the grant

## The assignment

Grant gr_cuobjlny6r (450k, due 2026-11-09), source Mitchell's decision 1 in mt_hlizi9wxxc. Steps 1 (as_pi5gjvlijz, server: GET /api/members, POST/DELETE /api/members/:userId/direct) and 2 (as_wnv254c2ro, web Let in + grant, Talk gating) are on main; read their reports (filing cabinet, search "direct work") and topic pages [dc_ckzkpsahhv](../../wiki/2026-10/2026-10-29-permissions-ask-to-join-member-kr-4-zkpsahhv.md) + [dc_ze5o8drnl9](../../wiki/2026-11/2026-11-01-user-stats-stand-town-hall-5o8drnl9.md) first. One commit on main, then park a live check.

Build:
1. Town Hall → User stats (web StatsPanel, see [dc_ze5o8drnl9](../../wiki/2026-11/2026-11-01-user-stats-stand-town-hall-5o8drnl9.md) for its layout and data) gains a Members table: one row per let-in member (login, let in when, direct-work goal text or "none"), with a one-click "Grant direct work under <goal>" (default: the viewer's captained goal, else the town goal for an admin) or "Revoke" for an admin or a captain over that goal. Clicking changes the row in place and the events feed logs it (kr_etn1l9ccpi). Non-admins see the table read-only or not at all, whichever the stand already does for its other sections.
2. Operating manual (docs/manual.md): one short line under the joining section saying a let-in member talks to managers only when an admin or captain grants "direct work under <goal>" (Let in card or User stats). The manual is capped under 1,900 words (packages/web/test/manual.test.ts): run check:docs, trim elsewhere for every word added.
3. Round trip: the outbox round-trip request dc_mgcbv3kqnd + add-on dc_fvlt8xajnz still describe Let in without the grant. File one new outbox request (request_human, kind observation) whose first line says it supersedes dc_fvlt8xajnz, with the full stranger round trip as it is now: Ask to join → Let in + direct work under <goal> → the member opens a 1:1 with Kelly → Kelly records a decision and a directed assignment with sourceId that 1:1 → acted rises by 1 (kr_t7rw103x6u, kr_bf2df18aa1). Note the new request id on [dc_ckzkpsahhv](../../wiki/2026-10/2026-10-29-permissions-ask-to-join-member-kr-4-zkpsahhv.md) for the continuation as_tunikdcd1g and the 7-day stop sc_gy1eruamog.

Web tests and typecheck pass. Then park a live check (submit_report resumeWhen {deploy: sha}): /api/health commit; mocked admin at 1400×900 shows the Members table with the grant button (cropped picture, recipe [dc_bci4l87ab6](../../wiki/2026-10/2026-10-29-live-verification-on-muster-town-i4l87ab6.md)), /api/manual has the new line, GET /api/members returns rows. Update [dc_ckzkpsahhv](../../wiki/2026-10/2026-10-29-permissions-ask-to-join-member-kr-4-zkpsahhv.md) and [dc_ze5o8drnl9](../../wiki/2026-11/2026-11-01-user-stats-stand-town-hall-5o8drnl9.md). When this is live and the key results all have live checks, say so in the report: Kelly closes the grant with close_grant.

## Proposal for next session

gr_cuobjlny6r step 3: User stats Members table with each member's direct-work goal and one-click grant/revoke; manual line; round-trip outbox add-on for the grant

Acknowledge to drop it, Continue to queue it again without the wait, or Redirect it with a note.
