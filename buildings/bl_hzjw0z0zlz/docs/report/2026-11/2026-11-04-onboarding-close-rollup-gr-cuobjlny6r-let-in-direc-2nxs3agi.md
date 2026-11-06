---
id: "dc_pj2nxs3agi"
type: "report"
state: "building"
title: "Onboarding close rollup: gr_cuobjlny6r (Let in → direct work) and gr_58n37j410s (after let-in) closed as done; 595,105 tokens returned; every piece is live, none used by a real member yet"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_wer2u0aisb","dc_ay5mjouteq"],"urls":[]}
tags: ["rollup"]
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-11-04T18:25:57.776Z"
sessionId: "se_32dx0su5fb"
createdAt: "2026-11-04T01:00:04.421Z"
updatedAt: "2026-11-04T18:25:57.776Z"
---
Live: 111e0bfd (server started 2026-11-04 00:53:17Z). Two grants closed this session so their key results reach you as one card.

## Shipped

**1. gr_cuobjlny6r closed as done: Let in → direct work under a goal, checked live**
**What it is:** The join path where a GitHub sign-in is read-only until an admin lets them in, with "Let in" / "Let in + direct work under <goal>" buttons, a Members table (Grant/Revoke direct work) on the User stats stand, and "Talk to ★" shown only to members holding direct work. The last two fixes (3914a437: Let in buttons wrap and Talk only where allowed; 824ab4d: Grant button no longer clipped) were re-checked on 111e0bfd by Kelly 1 with 6 mocked runs (admin, plain member, holder at 1400×900 and 390×844), 0 console errors ([dc_wer2u0aisb](2026-11-04-3914a437-and-824ab4d-live-and-checked-on-muster-to-r2u0aisb.md); evidence per key result on the topic page [dc_ckzkpsahhv](../../wiki/2026-10/2026-10-29-permissions-ask-to-join-member-kr-4-zkpsahhv.md)). Spent 950,081 / 1,500,000; 549,919 returned to the Bank.
**What you'd see:** As admin on muster.town/workshop/, an "asked to join" HUD notice with Let in, Let in + direct work under…, Decline on one card; User stats → Members table with Grant/Revoke per member ("Nobody has been let in yet" today). A plain member sees no Talk to ★ anywhere; a holder sees it on the manager panels and the You're in card. No picture: the mocked screenshots stay on the desk (no upload tool).
**Your call:** Mark the five key results from the in-tray. Four are claimed on live checks; kr_t7rw103x6u ("a holder opens a 1:1") is claimed only as "code live": no real holder has opened one yet, so missed is a fair mark if you want real use.

**2. gr_58n37j410s closed as done: You're in card, member 1:1 replies, "acted" funnel column**
**What it is:** The three pieces after let-in: the one-time "You're in" card, members' 1:1s with managers (and managers replying), and the public funnel's "acted" column. Kelly 2's evidence pass on 111e0bfd ([dc_ay5mjouteq](2026-11-04-gr-58n37j410s-evidence-the-features-are-live-and-m-5mjouteq.md)): manager replies are unblocked (1 spend-limit error since 11-02 02:00Z, the last at 2026-11-02T02:36:31Z; Nell and Pix replied to your 1:1s on 11-03), the card shows for a mocked let-in member, the funnel serves acted. Spent 704,814 / 750,000; 45,186 returned.
**What you'd see:** `curl https://muster.town/api/join-funnel` → 30-day guestCardViews 256, signIns 2, asked 1, letIn 1, declined 0, acted 0. All 18 1:1s since 10-31 are yours; nobody has been let in since you joined Hollyville on 10-29. API/data evidence only, no picture.
**Your call:** Mark the three key results: kr_xqbhxxptf3 (You're in card) is claimed from a mocked check; kr_e13rgsded6 (member 1:1 + reply) and kr_5xzxdvr1g5 (acted moves) are honestly not met yet because no real member exists; tokens can't buy that, which is why I closed rather than kept spending.

## Decided
- [dc_wer2u0aisb](2026-11-04-3914a437-and-824ab4d-live-and-checked-on-muster-to-r2u0aisb.md) (Kelly 1, re-check of 3914a437 + 824ab4d) → approve; nothing more to build.
- [dc_ay5mjouteq](2026-11-04-gr-58n37j410s-evidence-the-features-are-live-and-m-5mjouteq.md) (Kelly 2, gr_58n37j410s evidence pass) → approve (decided 00:56Z, folded here).

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_cuobjlny6r (closed done) | kr_v21y6z4tbv Let in + direct work buttons | claimed (live) | 950,081 / 1,500,000 |
| gr_cuobjlny6r | kr_etn1l9ccpi Members table Grant/Revoke | claimed (live) | |
| gr_cuobjlny6r | kr_qtmcpalo80 Talk only with direct work | claimed (live) | |
| gr_cuobjlny6r | kr_t7rw103x6u a real holder opens a 1:1 | claimed, code only; 0 real holders | |
| gr_cuobjlny6r | kr_3huiw2mea7 access test | claimed (CI green) | |
| gr_58n37j410s (closed done) | kr_xqbhxxptf3 You're in card | claimed (mocked) | 704,814 / 750,000 |
| gr_58n37j410s | kr_e13rgsded6 member 1:1 gets a reply | claimed, code only; 0 real members | |
| gr_58n37j410s | kr_5xzxdvr1g5 funnel "acted" moves | claimed, code only; acted 0 | |
| gr_fibsfwr4tz (funded) | kr_bf2df18aa1 stranger round trip | on-track, waiting on the outbox; final check sc_gy1eruamog 11-07 21:00Z | 407,049 / 450,000 |

Spend today by lane: exploration 0 tokens, directed 0 tokens. Building queue empty; no live forks.

## Needs from Mitchell
Nothing needed beyond the met/missed marks above. The whole Onboarding path is now blocked only on a real stranger being let in; the open outbox requests already ask you for that.

_Already waiting in your in-tray: 1 proposal (gr_zoo2cf2zpp), 4 requests ([dc_mgcbv3kqnd](../../../../../town-hall/outbox/2026-10/2026-10-31-one-real-join-round-trip-a-never-granted-github-ac-cbv3kqnd.md), dc_ulla3hu21p, dc_fvlt8xajnz, [dc_wtz7ltq8hf](../../../../../town-hall/outbox/2026-11/2026-11-03-add-on-to-the-join-round-trip-dc-mgcbv3kqnd-let-in-z7ltq8hf.md)), 5 rollups ([dc_u74lxukm10](2026-11-02-onboarding-rollup-2026-11-02-help-signs-done-membe-4lxukm10.md), [dc_tmz3tm7jox](2026-11-03-checkpoint-for-gr-ngg1z160a8-founder-road-cap-line-z3tm7jox.md), [dc_xf0b06vatn](2026-11-03-checkpoint-for-gr-cuobjlny6r-direct-work-under-goa-0b06vatn.md), [dc_66xza1ey0x](2026-11-03-onboarding-rollup-members-table-direct-work-grant-xza1ey0x.md), [dc_8t481sdm3e](2026-11-04-onboarding-close-rollup-gr-ngg1z160a8-founder-road-481sdm3e.md))._
