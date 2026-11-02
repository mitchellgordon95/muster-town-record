---
id: "dc_w600rbrf0t"
type: "report"
state: "building"
title: "Onboarding rollup 2026-10-26 (reply): key result kr_z0mj5teeu7 written and the stranger-path grant gr_cm3zha6mk6 filed on it (placeholder collective, Workshop under /workshop); Craig scoping the /workshop move"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_8zoikhz1fw","dc_g8pry6bugu","dc_5sbhq2iikw"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-26T15:48:56.569Z"
sessionId: "se_g26nxxweu4"
assignmentId: "as_h6jh09oipz"
costUsd: 2.3043387499999994
tokens: 17749
turns: 21
createdAt: "2026-10-26T15:48:36.857Z"
updatedAt: "2026-10-26T15:48:56.569Z"
---
## Shipped
Your reply on [dc_8zoikhz1fw](2026-10-26-onboarding-rollup-2026-10-26-budget-mode-default-c-oikhz1fw.md) (placeholder is fine; the current collective lives under /workshop) unblocked both open items. Nothing new on main; live commit 7ebf5ab.
- **Key result written** (kr_z0mj5teeu7, on the Onboarding board): "A stranger lands on muster.town, sees a homepage listing multiple collectives (the Workshop at /workshop plus a placeholder), opens one, signs in with GitHub, and sees other people live." Decision 1's wording plus your /workshop call; sources [dc_qg2gppz9jd](../../../../../library/meeting-notes/2026-10/2026-10-26-town-hall-town-hall-notes-2gppz9jd.md), [dc_8zoikhz1fw](2026-10-26-onboarding-rollup-2026-10-26-budget-mode-default-c-oikhz1fw.md), [dc_8k2pnlsya4](../../note/2026-10/2026-10-26-three-draft-key-results-for-the-onboarding-goal-pa-2pnlsya4.md). Main 7ebf5ab lets managers write key results, so I didn't wait for you to paste it. Keep or cut it.
- **Grant proposed**: gr_cm3zha6mk6 on that key result, 25 M tokens, in the Town Hall in-tray (draft was [dc_57jidmp9ks](../../note/2026-10/2026-10-26-draft-grant-the-stranger-path-homepage-of-collecti-jidmp9ks.md)). Four PRs, each live-checked by Craig before the next: (1) the client moves under /workshop with /api, /ws and /auth staying at the root so the OAuth callback and session cookie don't change, old root links redirect; (2) a collectives list + homepage at / listing the Workshop and a labelled placeholder (GET /api/collectives); (3) sign-in on a never-seen GitHub account; (4) multiplayer with two browsers. Five testing-plan lines, checkpoint at 50 %. Out of scope: a second real collective, multi-collective server, custom domains.
- **Craig assigned** (as_44w7l8j877, exploration on kr_z0mj5teeu7, under 2 M tokens): a scoping note, cited file:line, of everything that assumes the client lives at the root (Vite base, api.ts, auth redirects at auth/routes.ts:32 and :43, app.ts SPA fallback, README callback URL, Fly config) and the smallest change for the /workshop move and the homepage. No code; grant PR 1 starts from it once funded.
- A direct `tell` to you fails (your user id isn't an agent id), so replies reach you through rollups like this one.

## Decided
- [dc_8zoikhz1fw](2026-10-26-onboarding-rollup-2026-10-26-budget-mode-default-c-oikhz1fw.md) (your reply) → acted on as above. [dc_g8pry6bugu](2026-10-26-onboarding-rollup-2026-10-26-key-results-three-pas-pry6bugu.md) (key-result drafts) → superseded: KR 1 is written; KR 2 (first-timer explains the place in a minute) and KR 3 (new collective from the README in 15 min) stay drafts in [dc_8k2pnlsya4](../../note/2026-10/2026-10-26-three-draft-key-results-for-the-onboarding-goal-pa-2pnlsya4.md) until you want them. [dc_5sbhq2iikw](2026-10-26-stranger-path-grant-drafted-dc-57jidmp9ks-but-not-bhq2iikw.md) (parked draft) → done by this session.
- The parked continuation of as_wa6wrzz3vy (18:00Z) is now told, via my wiki, to confirm gr_cm3zha6mk6 exists and stop, not file a second proposal.

## Key results
kr_z0mj5teeu7: not-started, no funded grant yet (gr_cm3zha6mk6 proposed, 0 of 25 M spent). This session ~0.1 M tokens of directed work; Craig's note ≤2 M exploration.

## Needs from Mitchell
1. Fund, counter or reject gr_cm3zha6mk6 in the Town Hall in-tray (and keep or cut kr_z0mj5teeu7 if the wording is off).
2. By grant step 3: a GitHub account that has never signed in to muster.town, for the fresh-account and two-browser checks, or do those two checks yourself when Craig asks.

## Key results I wrote (keep or cut: Building → Settings → Key results)
- created kr_z0mj5teeu7: "A stranger lands on muster.town, sees a homepage listing multiple collectives (the Workshop at /workshop plus a placeholder), opens one, signs in with GitHub, and sees other people live (multiplayer)." (how to check: Private window on muster.town: two or more collectives listed; Open shows the Workshop at /workshop read-only; Sign in with a GitHub account that never signed in before works; a second browser signed in as another user sees that avatar move and a say bubble within 2 s.; from [dc_qg2gppz9jd](../../../../../library/meeting-notes/2026-10/2026-10-26-town-hall-town-hall-notes-2gppz9jd.md), [dc_8zoikhz1fw](2026-10-26-onboarding-rollup-2026-10-26-budget-mode-default-c-oikhz1fw.md), [dc_8k2pnlsya4](../../note/2026-10/2026-10-26-three-draft-key-results-for-the-onboarding-goal-pa-2pnlsya4.md))
