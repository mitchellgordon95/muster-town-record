---
id: "dc_xf0b06vatn"
type: "report"
state: "building"
title: "Checkpoint for gr_cuobjlny6r (direct work under <goal>): gate and two-button Let in card live, Members table on main; 3 of 5 key results claimed; 478,159 / 450,000; asking to continue with 80,000"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_8pf4r9o0ax","dc_fhe4d6qgf3","dc_fyfqvauwru","dc_ui31bdruwb","dc_3enaim4iq3"],"urls":["https://github.com/mitchellgordon95/agent-town/commit/92336d0e","https://github.com/mitchellgordon95/agent-town/commit/fc28a1e5","https://github.com/mitchellgordon95/agent-town/commit/df1cb9e5"]}
tags: ["rollup","checkpoint"]
verdict: "continue"
decision: "approve"
decidedBy: "system"
decidedAt: "2026-11-04T17:59:38.993Z"
sessionId: "se_fgra205tkx"
assignmentId: "as_k1h0kzf47n"
costUsd: 2.1490395
tokens: 107452
turns: 25
createdAt: "2026-11-03T03:30:53.919Z"
updatedAt: "2026-11-04T17:59:38.993Z"
---
Live: **6e6d663c** (server started 2026-11-03 03:27:30 UTC). It contains the grant's steps 1 and 2 (92336d0e, fc28a1e5). Step 3 (df1cb9e5) is on main with CI still running when I filed (run 41572063282). No pictures in this card: the two held live checks are what take them.

## Shipped

**1. Let in has two buttons: plain, or with "direct work under <goal>"**
**What it is:** On a pending Ask to join, the Town Hall in-tray row and the admin HUD notice show Let in (primary), Let in + direct work under <goal short name>, and Decline. The second one also grants the goal (your captained goal, or the town goal for an admin) in one call and logs "may direct work under …". Shared code in packages/web/src/panels/letIn.ts; server in 92336d0e (fc28a1e5, [dc_ui31bdruwb](2026-11-03-gr-cuobjlny6r-step-2-pushed-as-fc28a1e5-two-button-31bdruwb.md), [dc_fhe4d6qgf3](2026-11-02-gr-cuobjlny6r-step-1-direct-work-under-goal-gate-p-e4d6qgf3.md)).
**What you'd see:** muster.town Town Hall in-tray or the HUD notice the next time someone asks to join. Served bundle /workshop/assets/main-CGnAe6si.js contains "Let in + direct work" (2 hits). Nobody has asked to join since it landed, so it has only been pressed in tests. API-only evidence so far; the card pictures are the held check as_3eqwp4ujnw.
**Your call:** None.

**2. No permission, no 1:1: Talk to ★ follows the gate, the old member callout is gone**
**What it is:** A let-in member sees Talk to ★ only in buildings under a goal they may direct work under; elsewhere the manager's Talk tab shows one muted line saying who can grant that. The server refuses a non-holder's 1:1 and meeting with 403, and refuses their 1:1 or tell as a source of directed work (core canDirect, 92336d0e; web fc28a1e5).
**What you'd see:** Served bundle has 0 hits for "Members open one new 1:1 a day" and 1 for "is for people who direct work under". Signed out, POST /api/buildings/bl_hzjw0z0zlz/one-on-one returns 401; the 403 for a real non-holder is asserted by the server test, since no such member exists on the Workshop yet.
**Your call:** None.

**3. Members table on the user stats stand (on main, not yet live)**
**What it is:** Town Hall → user stats → a Members section for an admin or captain: each let-in member, when they were let in, their direct-work goals as chips with Revoke, or "none", and one primary Grant <goal> per member. Manual sentence updated (df1cb9e5, [dc_3enaim4iq3](2026-11-03-gr-cuobjlny6r-step-3-pushed-to-main-as-df1cb9e5-us-naim4iq3.md)).
**What you'd see:** Once CI deploys df1cb9e5: press E on the stats easel at the Town Hall, scroll past the funnel. Today the table would list the one let-in member. API-only until the held check as_vpdz73pnlc takes its picture.
**Your call:** None.

## Decided
- [dc_8pf4r9o0ax](2026-11-02-gr-cuobjlny6r-funded-plan-cut-into-3-grant-lane-st-f4r9o0ax.md) → approve (plan cut into 3 steps; all three shipped)
- [dc_fhe4d6qgf3](2026-11-02-gr-cuobjlny6r-step-1-direct-work-under-goal-gate-p-e4d6qgf3.md) → approve (step 1 on main as 92336d0e)
- [dc_fyfqvauwru](2026-11-03-92336d0e-live-direct-work-gate-deployed-ci-green-n-fqvauwru.md) → approve (92336d0e live-verified, CI green, named test passes)
- [dc_ui31bdruwb](2026-11-03-gr-cuobjlny6r-step-2-pushed-as-fc28a1e5-two-button-31bdruwb.md) → approve (step 2 on main as fc28a1e5; live check parked)
- [dc_3enaim4iq3](2026-11-03-gr-cuobjlny6r-step-3-pushed-to-main-as-df1cb9e5-us-naim4iq3.md) → approve (step 3 on main as df1cb9e5; redeploy queued)

## Key results
This grant: **478,159 / 450,000** tokens (106%). Due 2026-11-09.

| Key result | Status | How to check | What the check showed |
|---|---|---|---|
| kr_v21y6z4tbv Let in card: one click lets in + grants direct work | claimed | In-tray / HUD notice on a pending request shows both buttons; events after the second | Live in 6e6d663c; bundle contains "Let in + direct work" ×2; events asserted by access.test.ts:147; not yet pressed on a real request (no stranger since it landed) |
| kr_etn1l9ccpi Same grant/revoke from User stats | on-track | Town Hall → User stats → Members table, one-click Grant/Revoke, event logged | On main as df1cb9e5; CI run 41572063282 in progress at 03:27 UTC; web tests green (1,519); live check as_vpdz73pnlc held |
| kr_qtmcpalo80 Non-holder: no Talk, no callout, 403 | claimed | Member without grant sees no Talk to ★; bundle lacks "Members open one new 1:1 a day"; POST one-on-one → 403 | Bundle: 0 hits for the old line, 1 for the new one; signed-out POST → 401; 403 asserted by the server test (no non-holder member exists live) |
| kr_t7rw103x6u Holder 1:1 → directed assignment; first line counts as acted | on-track | Manager assigns directed work with sourceId = the 1:1; join-funnel acted +1 | Server half live and tested; no real holder exists yet; funnel 30 d: 210 views / 2 sign-ins / 1 asked / 1 let in / 0 acted; human half is outbox [dc_wtz7ltq8hf](../../../../../town-hall/outbox/2026-11/2026-11-03-add-on-to-the-join-round-trip-dc-mgcbv3kqnd-let-in-z7ltq8hf.md) |
| kr_3huiw2mea7 Gate tested, CI green | claimed | CI green on main; access.test.ts 'direct work permission gates 1:1s, meetings and directed sources' present and passing | Present at access.test.ts:147, passes; CI green on 92336d0e; df1cb9e5's run still in progress |

Other funded grants, unchanged this session: gr_fibsfwr4tz 407,049 / 450,000 (kr_pxisdsocdp, kr_a32db87f39, kr_fbef01cccb, kr_4395ff116f live and checked earlier; kr_bf2df18aa1 round trip not done, last check 2026-11-07); gr_58n37j410s 665,032 / 500,000 at checkpoint (kr_e13rgsded6 at-risk, kr_xqbhxxptf3 and kr_5xzxdvr1g5 on-track); gr_ngg1z160a8 408,681 / 250,000 at checkpoint (kr_z7sh9b4kxr, kr_9c3iz1ih4s claimed; kr_mw367chfbp on-track).

Spend today by lane: exploration 0 tokens (free under the goal: 0), directed 0 tokens.

## Needs from Mitchell
1. Continue this grant with a top-up of about 80,000 tokens: it runs the two held live checks (card pictures at both sizes; the Members table live with Grant/Revoke pressed on a mocked member) and then closes the grant with evidence per key result. If you'd rather cut it, the three claimed key results stand as they are and I cancel the two held checks; the Members table still goes live on its own once CI is green. The last key result's human half needs a stranger to ask to join, not tokens.

_Already waiting in your in-tray: 0 proposals, 4 requests (dc_mgcbv3kqnd, dc_ulla3hu21p, dc_fvlt8xajnz, [dc_wtz7ltq8hf](../../../../../town-hall/outbox/2026-11/2026-11-03-add-on-to-the-join-round-trip-dc-mgcbv3kqnd-let-in-z7ltq8hf.md)), 2 rollups ([dc_u74lxukm10](2026-11-02-onboarding-rollup-2026-11-02-help-signs-done-membe-4lxukm10.md), [dc_tmz3tm7jox](2026-11-03-checkpoint-for-gr-ngg1z160a8-founder-road-cap-line-z3tm7jox.md))._
