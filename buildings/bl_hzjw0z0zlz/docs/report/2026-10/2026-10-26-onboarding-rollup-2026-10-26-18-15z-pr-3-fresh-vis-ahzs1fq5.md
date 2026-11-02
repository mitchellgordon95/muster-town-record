---
id: "dc_ulahzs1fq5"
type: "report"
state: "building"
title: "Onboarding rollup 2026-10-26 18:15Z: PR 3 (fresh-visitor sign-in + two-user presence) pushed as eac2e24, redeploy queued; needs a real-GitHub check from Mitchell; KR 3 README exploration started"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_1jeze0cv5i","dc_p2ox3bqthe","dc_stoqzreczb","dc_pywgsgc8ve"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-26T18:13:07.836Z"
sessionId: "se_0g2a46mpez"
createdAt: "2026-10-26T18:06:38.245Z"
updatedAt: "2026-10-26T18:13:07.836Z"
---
## Shipped
- **PR 3 of the stranger path, eac2e24 on main** (Craig, [dc_1jeze0cv5i](2026-10-26-pr-3-pushed-to-main-as-eac2e24-fresh-visitor-signs-eze0cv5i.md)): a never-seen GitHub login goes homepage → Open → /workshop/ overlay → Sign in → back to /workshop/ signed in as role visitor with a human avatar, no admin UI. Tested locally through the real /auth/github callback path with a mock GitHub server and two headless browsers. Presence between two users measured locally: moves seen in 0.1–0.7 s (median ~0.3 s), says in 0.1–1.1 s, inside the 2 s target. Two fixes: guest loads no longer log a 404 for /api/dev/admin-token and a 401 for /api/me (GET /api/auth/config now returns dev and session); two newcomers no longer spawn on the same plaza tile. Tests green (core 268, server 73, runtime 119). Redeploy queued; Craig's parked continuation live-checks eac2e24 once it is up.
- **Style-guide skill** muster-style-guide [dc_q736158pnn](../../skill/2026-10/2026-10-26-muster-style-guide-36158pnn.md) written from the How-this-works overlay's theme and pinned for Onboarding ([dc_p2ox3bqthe](2026-10-26-reply-done-style-guide-skill-muster-style-guide-dc-ox3bqthe.md), confirmed [dc_stoqzreczb](2026-10-26-style-guide-skill-confirmed-muster-style-guide-dc-oqzreczb.md)). PR 4 (homepage pitch modal + square tiles with live town previews, Craig as_tzhxtwc9gh) follows PR 3 and uses it.

## Decided
- [dc_1jeze0cv5i](2026-10-26-pr-3-pushed-to-main-as-eac2e24-fresh-visitor-signs-eze0cv5i.md) (Craig, PR 3) → approve; its parked continuation does the live check, PR 4 is next in his queue.
- [dc_p2ox3bqthe](2026-10-26-reply-done-style-guide-skill-muster-style-guide-dc-ox3bqthe.md) (my reply on your rollup note: style guide) → approve.
- [dc_stoqzreczb](2026-10-26-style-guide-skill-confirmed-muster-style-guide-dc-oqzreczb.md) (style-guide pin confirmed, no changes) → approve.
- [dc_pywgsgc8ve](2026-10-26-stranger-path-grant-ask-closed-the-key-result-kr-z-wgsgc8ve.md) (stranger-path grant ask closed: gr_cm3zha6mk6 is already funded against kr_z0mj5teeu7, no duplicate proposal) → approve.
- New: KR 3 exploration as_2d0poxouo5 assigned to me (exploration lane, under 1.5 M): a timed fresh-clone walk of the README creating a second collective and its first coding building, listing the gaps and a draft grant for kr_tzg9en02dh.

## Key results
- kr_z0mj5teeu7 stranger path, gr_cm3zha6mk6: not-started on the goal (I'll move it on-track at the checkpoint); PRs 1–3 of 4 on main, PRs 1–2 live-verified; spend ~9.0 M / 25 M.
- kr_1rpq0738sw first minute, gr_vfyih8s6ri: on-track; at checkpoint ([dc_5mu02hanz3](2026-10-26-checkpoint-gr-vfyih8s6ri-kr-2-first-screen-054fdcf-u02hanz3.md)), 4.55 M / 4 M; still recommending you close it as done rather than top up.
- kr_tzg9en02dh new collective from the README: not-started, no grant; exploration under way (today's exploration 2.2 M / 6.3 M used before this).

## Needs from Mitchell
1. **A real-GitHub check of eac2e24 once it is live (about 5 min, two accounts or one plus a private window):** sign in with an account that never signed in → lands on /workshop/ signed in, /api/me shows role visitor and an avatarAgentId; two browsers see each other walk within ~2 s and see a typed message as a bubble; your admin session still opens the Town Hall in-tray and planning desk. (The OAuth app callback should still be https://muster.town/auth/github/callback; PR 1 did not change it.) Your friends' multiplayer test this week would cover the two-user part.
2. Decision on the KR 2 checkpoint [dc_5mu02hanz3](2026-10-26-checkpoint-gr-vfyih8s6ri-kr-2-first-screen-054fdcf-u02hanz3.md) (close gr_vfyih8s6ri as done).
