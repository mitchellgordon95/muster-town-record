---
id: "dc_6yjiriakvr"
type: "report"
state: "building"
title: "Onboarding rollup 2026-10-26 21:30Z: permissions design filed (Tae), build underway on main; new key result kr_pxisdsocdp for Mitchell to keep or cut; one decision: admin-only lets people in, or may members invite?"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_p6i1vm9ljs"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-26T22:05:24.381Z"
sessionId: "se_kgnr8ugx3z"
createdAt: "2026-10-26T21:25:18.124Z"
updatedAt: "2026-10-26T22:05:24.381Z"
---
## Shipped
Nothing new live since the 21:15Z checkpoint rollup ([dc_ek5ktlnwgi](2026-10-26-onboarding-checkpoint-2026-10-26-21-15z-gr-ibccoje-5ktlnwgi.md)). Filed in the building: Tae's design note [Design: who may interact with the town](../../note/2026-10/2026-10-26-design-who-may-interact-with-the-town-request-acce-cumcfubk.md), answering your flag [dc_hsdvn0h5ho](../../flag/2026-10/2026-10-26-not-anyone-who-logs-in-with-github-should-be-able-dvn0h5ho.md). Five lines: a new town role `member` with permission `town.interact` (admin, moderator and deployer have it; anyone who already holds a non-visitor role becomes member at startup); one preHandler in server/src/app.ts gates every non-GET from a user or a user-owned agent, plus WS move/say, reads never gated; a signed-in visitor sees one **Ask to join** button with an optional one-line message on the guest card; requests land in the **Town Hall in-tray** (not the mod station, which agents staff); **Let in / Decline** there needs `town.manage_roles`, and the person sees the answer on their next load.

## Decided
- [dc_p6i1vm9ljs](2026-10-26-permissions-half-1-design-note-filed-dc-f0cumcfubk-i1vm9ljs.md) (Tae, permissions half 1) → **continue**: Tae builds it on main now (as_0796022rpa, ~3 M cap, tests + VITE_MOCK screenshots, no redeploy until I queue it). Build assumes admin-only; if you say members may invite, that becomes a small follow-up.
- Wrote key result **kr_pxisdsocdp**: "A stranger who signs in with GitHub is read-only until Mitchell lets them in: Ask to join on the guest card → Town Hall in-tray → Let in → can walk, talk and message agents." Sources [dc_p6i1vm9ljs](2026-10-26-permissions-half-1-design-note-filed-dc-f0cumcfubk-i1vm9ljs.md), [dc_hsdvn0h5ho](../../flag/2026-10/2026-10-26-not-anyone-who-logs-in-with-github-should-be-able-dvn0h5ho.md). Keep or cut; no grant proposed yet (the build runs on your directed flag).

## Key results
- gr_ibccoje227 (KR 3 kr_tzg9en02dh): at checkpoint, held, 4,861,957 / 8,000,000 tokens, on-track (checkpoint [dc_ek5ktlnwgi](2026-10-26-onboarding-checkpoint-2026-10-26-21-15z-gr-ibccoje-5ktlnwgi.md) pending your continue/adjust/cut). Craig's README fix PR as_nuje3kqs67 is held behind it.
- KR 1 kr_z0mj5teeu7, KR 2 kr_1rpq0738sw: on-track, no grant. KR 1's open items (private-repo links 404, /?query 302) still in [dc_n7rm874dw4](2026-10-26-onboarding-rollup-2026-10-26-19-30z-76c6ad1-live-a-rm874dw4.md).
- Exploration today: 6,025,751 / 10,428,571.

## Needs from Mitchell
1. Decide: are you the only one who lets people in, or may members invite others too? The build assumes only you (grant = admin's `town.manage_roles`).
2. Keep or cut kr_pxisdsocdp (and continue/cut gr_ibccoje227 at its checkpoint, [dc_ek5ktlnwgi](2026-10-26-onboarding-checkpoint-2026-10-26-21-15z-gr-ibccoje-5ktlnwgi.md)).

## Key results I wrote (keep or cut: Building → Settings → Key results)
- created kr_pxisdsocdp: "A stranger who signs in with GitHub is read-only until Mitchell lets them in: they ask to join from the guest card, the request shows in the Town Hall in-tray, and after "Let in" they can walk, talk and message agents." (how to check: Private window on muster.town, sign in with a GitHub account that has never been granted a role: Ask to join is the one button on the guest card; moving or messaging an agent is refused. Mitchell clicks Let in in the Town Hall in-tray; on the next load the same account can move, say and message.; from [dc_p6i1vm9ljs](2026-10-26-permissions-half-1-design-note-filed-dc-f0cumcfubk-i1vm9ljs.md), [dc_hsdvn0h5ho](../../flag/2026-10/2026-10-26-not-anyone-who-logs-in-with-github-should-be-able-dvn0h5ho.md), [dc_f0cumcfubk](../../note/2026-10/2026-10-26-design-who-may-interact-with-the-town-request-acce-cumcfubk.md))
