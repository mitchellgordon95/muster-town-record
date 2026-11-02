---
id: "dc_glnso66daa"
type: "report"
state: "building"
title: "Onboarding rollup 2026-11-01 01:17Z: the stranger's road from sign-in to member is honest and measurable (gr_fibsfwr4tz steps 1–3 live), README one-pool Bank wording live; the real round trip waits on a human; after-let-in proposal filed"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_vxvrifkn5g","dc_2dqx4ijtvh","dc_hgzo91wakz","dc_7vt6cq2mfw","dc_xged9xi6ku","dc_u9yg6rl63h","dc_fpu1dxqo0r","dc_j9tfnw2rzl","dc_u32bynk4g1","dc_idleq5rdag","dc_5jyjfmt6gb","dc_prngc1gsjg"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-11-01T01:37:08.703Z"
sessionId: "se_xxjmz82s6n"
createdAt: "2026-11-01T01:19:48.668Z"
updatedAt: "2026-11-01T01:37:08.703Z"
---
Live: c1cdd23 (since 2026-11-01 01:07 UTC). It contains all of ours below: e8bd323, 66315ea, c321046 (checked live inside 00bf7ff at 2026-10-31 21:46 UTC) and 0e1c3b0 (checked inside 08a9831).

## Shipped

**1. The guest card tells the truth, and a pending request can't sit unseen**
**What it is:** gr_fibsfwr4tz steps 1 and 2. The signed-out guest card no longer promises "talk, review and join meetings"; it says sign-in lets you ask to join and an admin lets you in. The pending card names who decides (you) and the typical wait once any request has been decided. Admins get a HUD notice per pending request, "@login asked to join (Nm ago)", with Let in / Decline. Commits e8bd323, 66315ea; reports [dc_u9yg6rl63h](../2026-10/2026-10-31-gr-fibsfwr4tz-step-1-honest-guest-and-pending-card-yg6rl63h.md), [dc_fpu1dxqo0r](../2026-10/2026-10-31-gr-fibsfwr4tz-step-1-live-honest-guest-and-pending-u1dxqo0r.md), [dc_idleq5rdag](../2026-10/2026-10-31-gr-fibsfwr4tz-step-2-live-admins-see-login-asked-t-leq5rdag.md).
**What you'd see:** Private window on muster.town/workshop/: the new guest card. Signed in as you with a pending request: the notice under HUD Notices (today there are 0 pending; the only round trip ever was yours on Hollyville, decided in 15 s). Manual "Joining" and README match; manual at 1,898 / 1,900 words.
![Guest and pending cards](/api/media/mf_2hn0azbxmn.png)
**Your call:** None.

**2. A public join funnel: how many strangers get through each step**
**What it is:** gr_fibsfwr4tz step 3. Daily anonymous counts (guest-card views, GitHub sign-ins, asked, let in, declined, median time to decision) in one additive table (migration 073, back-filled from events and access requests), served at GET /api/join-funnel for the Workshop and every hosted collective, and shown as one row under the Dashboard KPI tiles. Commit c321046; reports [dc_j9tfnw2rzl](../2026-10/2026-10-31-join-funnel-pushed-to-main-c321046-counts-at-the-s-tfnw2rzl.md), [dc_5jyjfmt6gb](../2026-10/2026-10-31-gr-fibsfwr4tz-step-3-live-api-join-funnel-back-fil-yjfmt6gb.md).
**What you'd see:** curl https://muster.town/api/join-funnel, or the ▤ Dashboard row. Live totals, last 30 days: 2 sign-ins, 1 asked, 1 let in, median decision 15 s (Hollyville, n = 1); Workshop 1 sign-in, 0 asked. Guest-card views (about 105) are inflated by our own headless checks, and the view ping is unauthenticated, so treat that column as rough.
![Dashboard join-funnel row](/api/media/mf_dggb2kub1v.png)
**Your call:** None.

**3. README, self-host and hosted docs describe the one-pool Bank**
**What it is:** The first-collective funding steps (README step 6, docs/self-host.md §4, docs/hosted-collectives.md "First building") no longer name "Fund Lab", "Exploration / day" or a daily allowance; they say exploration starts by itself on the Bank's free tokens. Commit 0e1c3b0 (docs only, no picture); reports [dc_hgzo91wakz](../2026-10/2026-10-31-readme-step-6-self-host-step-4-and-the-hosted-firs-zo91wakz.md), [dc_7vt6cq2mfw](../2026-10/2026-10-31-0e1c3b0-is-live-readme-step-6-self-host-4-and-host-t6cq2mfw.md).
**What you'd see:** github.com/mitchellgordon95/muster-town README "Run it" step 6: "Donate to the Bank" and "Exploration starts by itself".
**Your call:** None.

Also: step 4 of the grant, one real round trip by a never-granted GitHub account, is an outbox request you already have; the fork checking it resumes in about 20 hours and stops honestly after 7 days with the funnel numbers if nobody does it. Kelly 1's exploration found that a member who is let in still reaches no one (no 1:1, no flag, a Say wakes nobody; the "You're in" toast is lost if they were away) and filed a proposal for it that is in your in-tray. The Workshop now runs the daily onboarding staleness sweep (its grant gr_mjr7nb438v, 19:00 UTC); Onboarding keeps the meaning side and mirrors each checked-through sha (sweep 5 = 63ed49e, mirror queued as as_gjbeer3nrv).

## Decided
- [dc_vxvrifkn5g](../2026-10/2026-10-31-gr-vj294o62x8-rejected-without-a-note-not-re-propo-vrifkn5g.md) → approve (gr_vj294o62x8 rejected: not re-proposed, doc fix queued as exploration)
- [dc_2dqx4ijtvh](../2026-10/2026-10-31-kr-4-s-ask-to-join-has-never-been-used-by-a-strang-qx4ijtvh.md) → approve (KR 4 never used by a stranger; proposed gr_fibsfwr4tz, which you funded)
- [dc_hgzo91wakz](../2026-10/2026-10-31-readme-step-6-self-host-step-4-and-the-hosted-firs-zo91wakz.md) → approve (0e1c3b0 pushed)
- [dc_7vt6cq2mfw](../2026-10/2026-10-31-0e1c3b0-is-live-readme-step-6-self-host-4-and-host-t6cq2mfw.md) → approve (0e1c3b0 live, 3/3)
- [dc_xged9xi6ku](../2026-10/2026-10-31-gr-fibsfwr4tz-funded-plan-cut-into-4-steps-on-the-ed9xi6ku.md) → approve (grant cut into 4 steps)
- [dc_u9yg6rl63h](../2026-10/2026-10-31-gr-fibsfwr4tz-step-1-honest-guest-and-pending-card-yg6rl63h.md) → approve (step 1 pushed e8bd323)
- [dc_fpu1dxqo0r](../2026-10/2026-10-31-gr-fibsfwr4tz-step-1-live-honest-guest-and-pending-u1dxqo0r.md) → approve (step 1 live, 0 console errors)
- [dc_j9tfnw2rzl](../2026-10/2026-10-31-join-funnel-pushed-to-main-c321046-counts-at-the-s-tfnw2rzl.md) → approve (step 3 pushed c321046)
- [dc_u32bynk4g1](../2026-10/2026-10-31-gr-fibsfwr4tz-step-4-round-trip-request-filed-dc-m-2bynk4g1.md) → approve (step 4 outbox request filed, continuation parked to 2026-11-01 21:00 UTC; 7-day check scheduled sc_gy1eruamog)
- [dc_idleq5rdag](../2026-10/2026-10-31-gr-fibsfwr4tz-step-2-live-admins-see-login-asked-t-leq5rdag.md) → approve (step 2 live, admin notice verified with a mocked request)
- [dc_5jyjfmt6gb](../2026-10/2026-10-31-gr-fibsfwr4tz-step-3-live-api-join-funnel-back-fil-yjfmt6gb.md) → approve (step 3 live, back-fill as predicted)
- [dc_prngc1gsjg](2026-11-01-explore-a-let-in-member-s-talk-reaches-no-one-prop-ngc1gsjg.md) → approve (after-let-in findings; proposal gr_58n37j410s in your in-tray; nothing queued until you decide)

## Key results
Grant gr_fibsfwr4tz, 356,762 / 450,000 tokens spent. Statuses are the town's (only you mark met); the evidence column is ours.

| Key result | Status | Evidence |
|---|---|---|
| kr_a32db87f39 signed-out guest card no longer promises talk/review/meetings | not-started (town); live and checked | e8bd323, [dc_fpu1dxqo0r](../2026-10/2026-10-31-gr-fibsfwr4tz-step-1-live-honest-guest-and-pending-u1dxqo0r.md): served bundle has "Sign in to ask to join", not the old line |
| kr_4395ff116f pending request visible to an admin with its age | not-started (town); live and checked | 66315ea, [dc_idleq5rdag](../2026-10/2026-10-31-gr-fibsfwr4tz-step-2-live-admins-see-login-asked-t-leq5rdag.md): HUD notice "@login asked to join (7m ago)" + Let in / Decline (mocked) |
| kr_fbef01cccb join funnel counts public and move | not-started (town); live, "moves" untested | c321046, [dc_5jyjfmt6gb](../2026-10/2026-10-31-gr-fibsfwr4tz-step-3-live-api-join-funnel-back-fil-yjfmt6gb.md): GET /api/join-funnel back-fill matches events; +1 on a real Ask waits on step 4 |
| kr_bf2df18aa1 real round trip done once | not-started | waits on the outbox request; fork resumes 2026-11-01 21:00 UTC, 7-day stop 2026-11-07 |
| kr_pxisdsocdp stranger read-only until let in, then can walk, talk, message | not-started | gates live since a5026c3 (code check 5/5); the live proof is the same round trip |

Spend by lane today: exploration 34,523 tokens (free under the goal: 9,745,184); directed 0 tokens.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 1 proposal (gr_58n37j410s), 1 request ([dc_mgcbv3kqnd](../../../../../town-hall/outbox/2026-10/2026-10-31-one-real-join-round-trip-a-never-granted-github-ac-cbv3kqnd.md)), 0 rollups._
