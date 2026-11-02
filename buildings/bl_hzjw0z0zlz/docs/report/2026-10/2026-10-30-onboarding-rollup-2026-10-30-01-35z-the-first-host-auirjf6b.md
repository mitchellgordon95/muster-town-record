---
id: "dc_f6auirjf6b"
type: "report"
state: "building"
title: "Onboarding rollup 2026-10-30 01:35Z: the first hosted collective exists (Hollyville, made by Mitchell's friend), gr_rdyrjzclfe closed as done at 974 k / 1 M and its key result claimed; KR 2 fixes live; one slug-case nit queued"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_nciijcryxq","dc_cijgmc4asa","dc_u97y0oar1o"],"urls":["https://muster.town/hollyville/","https://muster.town/api/collectives"]}
tags: ["rollup","grant-close"]
verdict: "stop"
decision: "approve"
decisionNote: "i think we're ok for now"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-30T02:10:50.194Z"
sessionId: "se_duin9cn0fr"
assignmentId: "as_g1v27yx7dp"
costUsd: 2.8454191499999997
tokens: 56908
turns: 41
createdAt: "2026-10-30T01:29:22.702Z"
updatedAt: "2026-10-30T02:10:50.194Z"
---
Live commit 5b89ea3 at 01:25Z; hosted.count 1.

## Shipped
**1. Hosted collectives: the first stranger-made collective is live, grant gr_rdyrjzclfe closed as done**
**What it is:** Your friend started Hollyville from the homepage (your answers [dc_c1vj3liowq](../../../../../library/human-report/2026-10/2026-10-30-re-create-the-demo-hosted-collective-on-muster-tow-vj3liowq.md), [dc_6op5uegvku](../../../../../library/human-report/2026-10/2026-10-30-re-start-fund-and-retire-a-collective-with-a-secon-p5uegvku.md), [dc_qztxk06ez8](../../../../../library/human-report/2026-10/2026-10-30-re-sign-in-once-on-muster-town-and-confirm-your-ro-txk06ez8.md); your flag [dc_1kylouq1l7](../../../../workshop/docs/flag/2026-10/2026-10-29-i-just-had-my-friend-make-a-collective-i-visited-a-ylouq1l7.md): you joined it and he approved you). That is the key result kr_7316be4jqw as written (a signed-in stranger starts a collective at muster.town/<name>, is its admin, it is listed, the Workshop untouched), so I closed the grant at 974,437 of 1,000,000 tokens; 25,563 go back to the Bank and the key result is claimed. The two race nits from your flag were fixed by the Workshop (75f6b5c live). Not exercised yet: a hosted collective running agents on its own API key; Hollyville has no key, so its funding reads "none".
**What you'd see:** muster.town/ shows two tiles, Workshop Collective (4 working now) and Hollyville "Make money" (Resting now); muster.town/hollyville/ loads; /hollyville/api/health says ok, funding none; /api/health hosted.count 1.
![Homepage tiles: Workshop Collective and Hollyville](/api/media/mf_qi6rj9m0oj.png)
**Your call:** Mark kr_7316be4jqw met or missed from this close report.

**2. First minute (KR 2): the phone guest card and insider words, c38f9b6 live**
**What it is:** The re-audit fixes ([dc_cijgmc4asa](2026-10-29-kr-2-re-audit-fixes-on-main-as-c38f9b6-phone-guest-jgmc4asa.md)): the guest card on a phone shrank from 53% to 34% of the screen, guests see no token or budget lines, touch screens say "Tap". Live check passed 5/5 ([dc_u97y0oar1o](2026-10-29-c38f9b6-is-live-and-the-check-passed-5-5-the-phone-7y0oar1o.md)).
**What you'd see:** muster.town/workshop/ in a private window at phone width: the guest card leaves two thirds of the map visible; no budget talk until you sign in.
**Your call:** None.

## Decided
- [dc_nciijcryxq](2026-10-29-sweep-4-e82afb7-is-live-5-5-pass-sweep-skill-repla-iijcryxq.md) (sweep 4 e82afb7 live, 5/5; sweep skill [dc_kzuf6rx4la](../../skill/2026-10/2026-10-29-onboarding-staleness-sweep-2-uf6rx4la.md) replaces Craig's) → approve.
- [dc_cijgmc4asa](2026-10-29-kr-2-re-audit-fixes-on-main-as-c38f9b6-phone-guest-jgmc4asa.md) (KR 2 fixes c38f9b6 on main) → approve, live check parked.
- [dc_u97y0oar1o](2026-10-29-c38f9b6-is-live-and-the-check-passed-5-5-the-phone-7y0oar1o.md) (c38f9b6 live, 5/5) → approve.
- Your three answers [dc_c1vj3liowq](../../../../../library/human-report/2026-10/2026-10-30-re-create-the-demo-hosted-collective-on-muster-tow-vj3liowq.md), [dc_6op5uegvku](../../../../../library/human-report/2026-10/2026-10-30-re-start-fund-and-retire-a-collective-with-a-secon-p5uegvku.md), [dc_qztxk06ez8](../../../../../library/human-report/2026-10/2026-10-30-re-sign-in-once-on-muster-town-and-confirm-your-ro-txk06ez8.md) (Hollyville exists, checklist works) → gr_rdyrjzclfe closed as done; one directed assignment queued: as_fmjf5ge1ud makes muster.town/Hollyville (as you typed it) redirect to /hollyville/ instead of bouncing silently to the homepage.

## Key results
| Key result | Status | Grant | Spent / granted |
|---|---|---|---|
| kr_7316be4jqw hosted collectives | claimed | gr_rdyrjzclfe closed done | 974,437 / 1,000,000 |
| kr_pxisdsocdp read-only until let in | not-started, no grant | your real join round trip in Hollyville is the evidence so far | – |
| kr_1rpq0738sw first minute | on-track, no grant | c38f9b6 live | – |
| kr_hee2pa2d5r staleness | on-track, no grant | sweep 4 live, sweep 5 adds the Hollyville facts | – |
Spend today: exploration 0 / 828,571 tokens; directed 0 tokens before this session (this session is directed and not counted yet).

## Needs from Mitchell
1. Say whether "a hosted collective runs its own agents on its owner's API key" (the funding and desk cost call you deferred) becomes the next Onboarding key result, or stays out of scope for now. One line is enough; I write the key result and propose a grant from it.

_Nothing else waiting in your in-tray._

## Reply from Mitchell (2026-10-30 02:10)

i think we're ok for now

