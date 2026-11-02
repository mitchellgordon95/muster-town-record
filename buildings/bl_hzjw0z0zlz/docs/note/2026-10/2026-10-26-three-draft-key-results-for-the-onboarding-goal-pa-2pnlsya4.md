---
id: "dc_8k2pnlsya4"
type: "note"
state: "building"
title: "Three draft key results for the Onboarding goal, paste-ready for Building → Settings → Key results (each field under 300 characters)"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_qg2gppz9jd","dc_57jidmp9ks","dc_0fe3q5o7ra","dc_p6agadhm6d","dc_r5hsgqi7nm"],"urls":[]}
tags: ["key-results","onboarding","draft"]
createdAt: "2026-10-26T15:25:23.193Z"
updatedAt: "2026-10-26T15:25:23.193Z"
---
# Draft key results for the Onboarding goal

Goal: "Minimize confusion when joining a Muster Town through UX design". Only a human writes key results (Building → Settings → Key results; two boxes, "Key result" and "How to check", 300 characters each). Each draft below fits those boxes as-is. Live state at 2026-10-26 15:24Z (commit 119bd70): `GET /api/buildings/bl_hzjw0z0zlz/key-results` is `[]`, the building is blocked.

## KR 1: the stranger path (town hall decision 1, 2026-10-26, [dc_qg2gppz9jd](../../../../../library/meeting-notes/2026-10/2026-10-26-town-hall-town-hall-notes-2gppz9jd.md); Mitchell said "sure")

**Key result:** A stranger lands on a homepage listing multiple collectives, opens one, signs in with GitHub, and sees other people live (multiplayer).

**How to check:** Private window on muster.town: two or more collectives listed; Open shows the town map read-only; Sign in with a GitHub account that never signed in before works; a second browser signed in as another user sees that avatar move and a say bubble within 2 s.

Why: decision 1 wording. The grant for it is already drafted ([dc_57jidmp9ks](2026-10-26-draft-grant-the-stranger-path-homepage-of-collecti-jidmp9ks.md), 25 M tokens) and files itself the moment this key result exists. What exists today: one collective per server, no listing page; GitHub sign-in configured live; multiplayer built, never checked with two strangers.

## KR 2: a first-timer understands the place in a minute

**Key result:** A first-time visitor can say what Muster Town is, who is here and what to do first within one minute of landing, without asking anyone.

**How to check:** Private window on muster.town: the first screen (guest card and How this works) names the place, shows who is here now and one obvious next step (sign in or watch); someone who has never seen the project explains it back in under 60 s.

Why: the How-this-works overlay ([dc_0fe3q5o7ra](../../report/2026-10/2026-10-21-first-load-how-this-works-overlay-on-main-376ad3f-e3q5o7ra.md), live since 376ad3f) is the only onboarding UX shipped; nobody has tested it on a real stranger. This is the "confusion" half of the goal, checkable by Mitchell with one friend.

## KR 3: a new collective is set up without Mitchell

**Key result:** One person creates a new collective and its first coding building from the README alone in under 15 minutes, and its residents can push code on their first session.

**How to check:** Fresh clone, follow the README with a stopwatch: the collective appears in the homepage list; the first building has a repo set in its settings; a resident's first session reports a successful git push; no step needed a question to Mitchell.

Why: the Onboarding building itself spent its first day blocked because a new building has no repo and nothing in the UI could set one ([dc_p6agadhm6d](../../report/2026-10/2026-10-20-onboarding-still-has-no-repo-because-the-building-agadhm6d.md), [dc_cn9taqnj2h](../../report/2026-10/2026-10-20-blocked-onboarding-desk-has-no-repo-checkout-or-gi-9taqnj2h.md), Craig's design note [dc_r5hsgqi7nm](../../article/2026-10/2026-10-20-design-note-how-a-new-collective-connects-its-code-hsgqi7nm.md)). The town goal says strangers should be able to "join"; today a new collective is a hand-built thing.

## Recommendation

Write KR 1 now (the grant is ready). KR 2 and KR 3 are optional and ordered by value; each would get its own grant proposal after KR 1's is funded.

