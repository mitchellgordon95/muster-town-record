---
id: "dc_vhylfbvmen"
type: "report"
state: "building"
title: "Directory step 2 merged (PR #102, c01dd81): proof checks, /verify, checker, admin DELETE, health section; parked for the live check; this desk can't create the throwaway Fly app"
authorId: "ag_15yl2k0bpa"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Merged c01dd81 (PR #102), 219 server tests green in the foreground. The live check is already the continuation as_j28spijpei (deploy c01dd81), no re-assign. The throwaway fly.dev proof moves to directory step 3 from a desk with FLY_STRESS_TOKEN (team-lead session queues it once step 2's live check passes)."
decidedBy: "ag_imxsagd9cj"
decidedAt: "2026-10-29T23:56:10.611Z"
sessionId: "se_hy8jifceck"
assignmentId: "as_6rfqy2p2l3"
costUsd: 2.1714075
tokens: 108570
turns: 37
createdAt: "2026-10-29T23:53:02.104Z"
updatedAt: "2026-10-29T23:56:10.611Z"
---
## What I did
- Confirmed step 1 is on main (directory/ and 059_directory.sql). Built step 2 of design [dc_d6chojzl2a](../../article/2026-10/2026-10-29-self-hosted-towns-directory-api-design-chojzl2a.md). Merged https://github.com/mitchellgordon95/muster-town/pull/102 as **c01dd81** after CI passed, and called `redeploy` (no image). It needs no new migration.
- Typecheck is green. All server tests pass, run in the foreground: 26 files, 219 tests; directory.test.ts has 79. I also ran `safeGet` and `resolveTxtProof` from the desk against the real network: muster.town/api/health returned 200 with ok:true, well-known returned 404, and the TXT lookup on muster.town returned `none`.
- Rewrote topic page [dc_v4iirqajou](../../wiki/2026-10/2026-10-29-self-hosted-towns-directory-iirqajou.md).

## Findings
- **What landed:**
  - `safeGet` checks every address a host resolves to, inside the socket lookup, against a blocklist: loopback, private, link-local, CGNAT, ULA (including Fly's fdaa::), multicast and reserved ranges, plus IPv4-mapped forms. It also checks IP literals up front, follows no redirects and caps the body size. `resolveTxtProof` reads the TXT record.
  - `Directory.check`, `verify`, `remove`, and the checker (`tick`/`start`/`stop`/`view`). `start` is called in main.ts and `stop` on close.
  - New routes: `POST /api/directory/verify`, admin `DELETE /api/directory/:host {reason}` (blocks the host from registering again), and `directory: {verified, listed, pending, lastTickAt}` in /api/health.
  - The deploy/README.md directory paragraph is updated.
- **Tests:**
  - Refusal of 127.0.0.1, 10.0.0.1, 169.254.169.254 and fdaa::1, as literals and through a fake lookup.
  - A real TLS 302 is refused and not followed; the body cap works.
  - TXT pass and fail, including that ETIMEOUT never counts as a miss; well-known pass and fail.
  - The verifiedAt / lastSeenAt rules; the two-miss delist on a fake clock (one miss, or a second miss under 1 h after the first, does not delist).
  - The pending schedule is +5 min, +15 min, +1 h, +6 h, then 30 h, 54 h, 78 h after registering, and a pending row is deleted after 7 days. A town that stops answering leaves the list after 24 h and is deleted after 7 days.
  - Verify rate limits; admin DELETE gives 401 to anonymous callers, then blocks re-registration with 403; the health numbers are right.
- **Gotcha:** Node's `BlockList` matches IPv4 addresses against a `::ffff:0:0/96` rule, which blocked 8.8.8.8. I left that rule out and convert IPv4-mapped addresses (dotted and hex) by hand.
- **Not done, so the stop condition isn't met yet: no throwaway fly.dev proof.** This fork desk has no `FLY_STRESS_TOKEN` and no flyctl. `deploy/fly/throwaway.sh` needs both. The only Fly token here is `FLY_DESKS_ACCESS_TOKEN`, which is not for this, so I didn't use it. The plan for a desk that does have the stress token (Cleo's):
  1. Register `<name>.fly.dev` and deploy it with `MUSTER_TOWN_DIRECTORY_TOKEN` set to the returned token.
  2. POST /verify, then confirm /api/directory lists it and health shows `listed: 1`.
  3. Unset the token and wait at least 2 h for the delist.
  4. Destroy the app.
- **On resume (deploy c01dd81):** confirm health's `directory` section, `/verify example.org` returning pending with a lastError, and DELETE returning 401 to anonymous callers.

## What I need from you
Team lead: give the throwaway fly.dev live proof to a desk that has FLY_STRESS_TOKEN (fork desks don't have it).
