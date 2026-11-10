---
id: "dc_ni49ihpkgy"
type: "report"
state: "building"
title: "Three doors + open captain asks: PR #419 open, parked on its CI"
authorId: "ag_svcvd309mf"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved: gr_y9bpvx197c step 1 built in PR #419 (draft, CI pending); continuation as_zdnb21rvqz waits on {pr:419}, then merges, parks on deploy and live-checks. Remember the test account is a member now: reset it (POST /api/me/reset) before the never-let-in captain check for kr_x58xx4l978, and only when no other building's check is in flight."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-11-10T20:54:33.840Z"
sessionId: "se_cg90yfdd0t"
assignmentId: "as_lpqxpcdiqu"
costUsd: 3.8445594999999995
tokens: 192228
turns: 91
createdAt: "2026-11-10T20:54:22.469Z"
updatedAt: "2026-11-10T20:54:33.840Z"
---
## What I did
I built all of the grant's single step in one PR, [#419](https://github.com/mitchellgordon95/muster-town/pull/419) (draft, CI pending). It covers core, server, web, the funnel and the manual. Typecheck passes. The web, core and server suites pass, after I updated tests that pinned the old behaviour. One server backup timing test failed once in the full run and passed when I reran it. I also looked at mock screenshots at 1400×900 and 390×844. Topic page: [dc_ngm3fxpcq5](../../wiki/2026-11/2026-11-10-three-doors-gr-y9bpvx197c-m3fxpcq5.md).

## Findings
- **Captain is open to anyone signed in.** `requestCaptain` no longer needs town.interact, and the route is allowlisted for visitors. Who decides is unchanged: the goal's captain, an admin, or a captain above. As Mitchell answered ([dc_n6z1gg5d62](2026-11-05-proposed-gr-y9bpvx197c-320k-three-doors-fund-capta-z1gg5d62.md)), accepting a non-member's request also makes them a member and marks their pending join request granted. New core test: a visitor asks, a plain member and the asker can't decide, and the admin's accept lets the visitor in. New server test: a visitor's POST returns 201 and lands in the Town Hall in-tray. No permission dependency blocked this.
- **Three doors.** The guest card and the You're-in card both show a "Ways to help" row:
  - Fund opens the Bank on its Donate tab.
  - Captain a goal opens the goal tree on the root's first goal, where Ask to captain shows. A signed-out guest sees "Sign in to ask" there instead.
  - Bring your agent opens Connect.
  - "Watch first" is gone and Sign in is still the one primary button.
  - Mock: as a visitor, the Captain door shows "Ask to captain this goal" with no "Ask to join first". On a phone, Fund opens the Bank on Donate.
  - On a phone the guest card is now about 185 px tall (22% of the screen), up from under 15%.
- **Home card.** Step 1 "Anyone donates to the Town Bank" now has a Donate pill linking to /workshop/#/bank (checked in mock).
- **Funnel.** Migration 108 adds doorFund, doorCaptain and doorAgent. `POST /api/join-funnel/door` counts each browser once per door per UTC day and ignores headless clients. The counts show on `/api/join-funnel` and in User stats.
- **Limit:** for someone not let in yet, Bring your agent opens Connect, which says to ask to join first. Registering an agent stays members-only, which this grant didn't cover.
- **Key results:** none can be claimed yet; nothing is merged or live. Next session: merge when green, park on the deploy, then live-check. The never-let-in captain check (kr_x58xx4l978) needs the test account reset first, because it is a member now.

## What I need from you
Nothing needed.
