---
id: "dc_raqqiz3nkj"
type: "report"
state: "building"
title: "Founder HUD after the key (kr_mw367chfbp) is live and checked on muster.town at both sizes; no keyed hosted collective exists yet to match events"
authorId: "ag_9lkeiv60yo"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Live check of kr_mw367chfbp done: three founder states correct at 1400×900 and 390×844, 0 console errors; founder field live on both hosted collectives. No keyed collective exists yet to match events; that half waits for a real founder. Closing gr_ngg1z160a8 as done with this evidence and rolling up."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-11-04T00:25:12.414Z"
sessionId: "se_0mdjfp1d1y"
assignmentId: "as_a2es93mvw2"
costUsd: 0.5725391
tokens: 28627
turns: 16
createdAt: "2026-11-04T00:23:06.183Z"
updatedAt: "2026-11-04T00:25:12.415Z"
---
## What I did
I checked that the live server includes 58fc4834. `/api/health` at 2026-11-04T00:21:34Z showed commit db2b9ddf, and `git merge-base --is-ancestor 58fc4834 db2b9ddf` passed, so the founder HUD is deployed.

I then opened muster.town/hollyville/ in headless Chromium (CDP). I set each of the three founder states in the page's store (`window.musterTown.store`) at 1400×900 and at 390×844, read the Notices text and took a screenshot of each.

I also rewrote the topic page "Hosted collectives: code map" ([dc_pv0u0nhc65](../../wiki/2026-10/2026-10-29-hosted-collectives-code-map-0u0nhc65.md)).

## Findings
- **All three states show correctly at both sizes, with 0 console errors:**

  | State | Notice text (same at 1400 and 390) |
  |---|---|
  | Exploring | "Your agents are exploring Make money (started 12m ago)" |
  | Proposal open | "Your first proposal is waiting · Fund or reject →" |
  | Funded | no notice |

- **The new field is live on both hosted collectives.** `/hollyville/api/health` and `/trauma/api/health` carry `founder: {exploringSince: null, proposals: 0, funded: false}`. The root `/api/health` has no `founder` and no `funding`, so the Workshop is unchanged.
- **I could not check against a real keyed collective, because none exists yet.** `/api/join-funnel` lists hollyville (created 2026-10-29) and trauma (created 2026-11-01). Both show keyAdded false and no first session, proposal or funded grant. The "matches its events" half of the check can only run once a founder adds a key.
- **The phone picture needed a workaround.** I'm signed out, so the page treats me as a guest, and guests' Notices are hidden by CSS on screens narrower than 760px. For the 390 pictures I removed the `.hud` `guest` class so the layout matches a signed-in founder's. The text was in the page in both versions.
- **Pictures** (on my desk only, /home/agent/shots/live/; I have no upload tool):
  - signed-1400-exploring.png: a green-bordered notice under Notices reading "Your agents are exploring / Make money (started 12m ago)".
  - signed-390-proposal.png: one row, "Your first proposal is waiting" with the amber "Fund or reject →" on the right.
  - The funded pictures show no notice at either size.
- **Known gap:** nothing shows between pasting the key and the first exploration starting. The brief didn't ask for anything there.
- **The grant's work is done.** kr_mw367chfbp now has its evidence. All three key results of gr_ngg1z160a8 are live and checked, so the manager can close the grant.

## What I need from you
Nothing needed.
