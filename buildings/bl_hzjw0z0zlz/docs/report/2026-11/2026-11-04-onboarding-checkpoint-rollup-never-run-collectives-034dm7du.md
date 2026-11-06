---
id: "dc_wi034dm7du"
type: "report"
state: "building"
title: "Onboarding checkpoint rollup: never-run collectives say so (gr_a6512x0je1) is on main but not yet live, 169,114 / 150,000 spent; a 40,000 top-up buys the live check and close. Also live in 0af4874: the help-sign tour and the join funnel's real-stranger counts"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_t236744daz","dc_wv8jp5o5jj","dc_tmvfyiako2","dc_snzjnokp45","dc_i39wsqtnj4","dc_1gpb1buwmr"],"urls":[]}
tags: ["rollup","checkpoint"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-11-05T20:01:06.084Z"
sessionId: "se_q673vjtktc"
assignmentId: "as_r8wbdgcn10"
costUsd: 2.1505517
tokens: 107528
turns: 20
createdAt: "2026-11-04T18:57:06.846Z"
updatedAt: "2026-11-05T20:01:06.084Z"
---
Live: **0af4874** (server started 2026-11-04 18:47:03Z). It contains the tour (eec2401) and the join-funnel counts (c5e0005a), not the never-run work (48d88720): main's deploy of it was in flight when this was filed, and a newer push restarted main's CI, so it lands with that run. No pictures: the live-check screenshots need an upload tool I don't have.

## Shipped

**1. A collective that has never run says so (on main, deploying)**
**What it is:** The grant's whole plan in one commit, 06575cee, merged as 48d88720. Every entry of the public collectives list now says whether the collective has ever run. A never-run collective's homepage tile reads "Not started yet: waiting for its founder's key." instead of "Resting now" and sorts after the collectives that have run. A signed-out visitor at a never-run collective (Hollyville, Trauma) is told it hasn't started and is pointed to the Workshop, in both the first-minute card and the guest card. The Workshop's own screens are unchanged. Unit tests cover the sorting, the tile markup, the health flag and the guest wording. Spend 169,114 of 150,000: the plan said one session; it took one long one plus this checkpoint.
**What you'd see:** Nothing yet. Today muster.town/ still shows Hollyville and Trauma as "Resting now" and muster.town/trauma/ still says "click any agent". Once a commit at or after ad27e6f4 is live: the Workshop tile first, "Not started yet" on the other two, and /trauma/ opening on a "Not started yet" page whose button is "Open Workshop Collective".
**Your call:** Continue with the 40,000-token top-up so the parked desktop + phone live check runs and closes the grant, or cut it now: the code deploys with main either way, but nobody will have checked it live.

**2. The help sign is a tour of the building (your flag)**
**What it is:** Your flag asked for the "?" sign's text to tour the building. Pressing a building's help sign now shadows the rest of the town, lights that building, and numbers each thing in it with a hotspot you hover or tap for its one-line description; Esc, the sign or the close button end it cleanly. PR #314 → eec2401, live since b228277 and still in 0af4874. Checked as a guest at 1400×900 and on a 390×844 phone ([dc_snzjnokp45](2026-11-04-help-sign-tour-is-live-on-muster-town-eec2401-in-b-zjnokp45.md)).
**What you'd see:** muster.town/workshop/ signed out: click the "?" sign in any building. Three small leftovers are logged for the next sweep: a tooltip near a building's top wall can cover a neighbouring hotspot, one line wraps on phone, and a phone guest's walk from the tour to the in-tray goes out the door and round.
**Your call:** None.

**3. The join funnel counts real strangers (live, API and User stats)**
**What it is:** The top of the join funnel no longer counts page loads. It counts distinct guest-card visitors per browser per day, homepage visitors the same way, and a press of Sign in even when the visitor quits at GitHub; headless browsers (our own checks) are skipped. c5e0005a, live in 0af4874; its own live check is parked and will close that grant.
**What you'd see:** curl https://muster.town/api/join-funnel: the new columns homeViews, guestVisitors and signInStarted are there and read 0 today (they started counting at 18:47Z; the old guestCardViews reads 614 over 30 days, mostly our own headless checks). Town Hall → User stats easel → E lists the three new columns with definitions.
**Your call:** None.

## Decided
- [dc_t236744daz](2026-11-04-explore-2-of-the-3-homepage-collectives-have-never-36744daz.md) → approve (Kelly 1's exploration: found 2 of 3 homepage collectives never ran; proposed this grant)
- [dc_wv8jp5o5jj](2026-11-04-gr-a6512x0je1-taken-whole-and-pushed-to-main-as-48-8jp5o5jj.md) → approve (the grant's plan pushed to main as 48d88720; live check parked)
- [dc_tmvfyiako2](2026-11-04-help-sign-tour-built-pr-314-lit-building-shadowed-vfyiako2.md) → approve (tour built, PR #314, parked on CI)
- [dc_snzjnokp45](2026-11-04-help-sign-tour-is-live-on-muster-town-eec2401-in-b-zjnokp45.md) → approve (tour live-checked on desktop and phone)
- [dc_1gpb1buwmr](2026-11-04-grant-gr-zoo2cf2zpp-adjusted-300-000-tokens-pb1buwmr.md) → approve (your adjust of the funnel grant to 300,000 recorded)
- [dc_i39wsqtnj4](2026-11-04-gr-zoo2cf2zpp-taken-whole-and-pushed-to-main-as-c5-9wsqtnj4.md) → approve (funnel counts pushed as c5e0005a; live check parked)

## Key results

**This checkpoint: gr_a6512x0je1, 169,114 / 150,000 tokens**

| Key result | Status | How to check | What the check showed |
|---|---|---|---|
| kr_6xv83q1k14 GET /api/collectives says started true/false | on-track (on main, not live) | curl https://muster.town/api/collectives | 0af4874 at 18:54Z: no started field yet; code in ad27e6f4, tests pass |
| kr_7pdn6k1w2r Never-run tiles read "Not started yet" and sort last | on-track (on main, not live) | Private window on muster.town/ | 0af4874 still shows "Resting now"; markup and sorting unit-tested |
| kr_fk7c0pdvvs Guest at a never-run collective is told so and pointed to the Workshop | on-track (on main, not live-checked) | Private window on muster.town/trauma/ at 1400×900 and on a phone | Wording unit-tested; the desktop + phone live check is the held continuation |

**Other funded grants**

| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_fibsfwr4tz | kr_pxisdsocdp read-only until let in | live | 407,049 / 450,000 |
| gr_fibsfwr4tz | kr_a32db87f39 guest card promises only sign-in | live | |
| gr_fibsfwr4tz | kr_fbef01cccb join funnel counts public | live | |
| gr_fibsfwr4tz | kr_4395ff116f pending request in HUD Notices | live | |
| gr_fibsfwr4tz | kr_bf2df18aa1 real round trip once | waiting on a real stranger (outbox request open; 7-day check 2026-11-07) | |
| gr_zoo2cf2zpp | kr_tsrsclo71o guestVisitors distinct, headless skipped | live in 0af4874, live check parked | 230,859 / 300,000 |
| gr_zoo2cf2zpp | kr_o5pvkvop0h signInStarted counted | live in 0af4874, live check parked | |
| gr_zoo2cf2zpp | kr_wy2r43djiw homeViews + User stats columns | live in 0af4874, live check parked | |

Spend today by lane: exploration 68,642 tokens (free under the goal 3,935,192); directed 151,656 tokens.

## Needs from Mitchell
1. Continue this checkpoint with the 40,000-token top-up (the parked live check on desktop and phone, then the close), or cut it: the code is on main and deploys either way; only the live check and the close are missing.
2. A word on the grant's stop condition: do you want never-run collectives labelled "Not started yet" (what shipped) or hidden from the homepage altogether? If hidden, say so and the top-up does that instead, as one change.

_Already waiting in your in-tray: 0 proposals, 4 requests ([dc_mgcbv3kqnd](../../../../../town-hall/outbox/2026-10/2026-10-31-one-real-join-round-trip-a-never-granted-github-ac-cbv3kqnd.md), dc_ulla3hu21p, dc_fvlt8xajnz, [dc_wtz7ltq8hf](../../../../../town-hall/outbox/2026-11/2026-11-03-add-on-to-the-join-round-trip-dc-mgcbv3kqnd-let-in-z7ltq8hf.md)), 0 rollups._
