---
id: "dc_h6ko9fvf56"
type: "report"
state: "building"
title: "Onboarding rollup 2026-10-27 21:00Z: hosted collectives step 2 (one sign-in) is live and verified; step 3 (Start a collective) parked until the deploy; Mitchell's `demo` fixture and one real GitHub sign-in are the two things waiting on him"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_9oka3bqhxb","dc_71kcxpueqf"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-27T22:49:54.124Z"
sessionId: "se_e0io7uecmw"
createdAt: "2026-10-27T21:17:36.037Z"
updatedAt: "2026-10-27T22:49:54.124Z"
---
## Shipped
- **Hosted collectives step 2, one sign-in (8ecf110), is live.** Live commit 086eeff contains it. Craig's live check ([dc_9oka3bqhxb](2026-10-27-hosted-collectives-step-2-live-check-8ecf110-is-li-ka3bqhxb.md), 25.5 k tokens) at 20:45Z: /workshop/ loads for an anonymous visitor with the sign-in guest card and 0 console errors; /api/me is 401; an unknown /<slug>/ redirects to /; `?return_to=https://evil.test/demo/` and `?return_to=/nope/` both go to GitHub with the signed state cookie carrying **no returnTo** (the bad value is dropped, the callback falls back to /workshop/), while `/workshop/` is kept. Nothing points off-site. Screenshot on Craig's desk: /home/agent/shots/hub2/1.png.
- What one sign-in does (for the demo): the root session cookie carries the GitHub identity; every hosted collective at /<slug>/ resolves it in its own World (guest on first visit, the creator admin), so opening /demo/ after signing in once asks for no second GitHub prompt.
- **Step 3 design** (Tae, [dc_71kcxpueqf](2026-10-27-hosted-collectives-step-3-parked-before-any-code-s-kcxpueqf.md) and dc_u7a6nt1fu0): Start a collective for any signed-in GitHub user, one active collective per GitHub id, Anthropic API key only stored as that World's Bank input and never returned, "No key yet" hold in the HUD, retire keeps the slug. No code yet: Tae parked before writing any so the 8ecf110 redeploy could go live; it resumes by itself after the deploy.

## Blockers and needs from Mitchell
1. **Create the `demo` collective** (outbox [dc_chdfylcjva](../../../../../town-hall/outbox/2026-10/2026-10-27-create-the-demo-hosted-collective-on-muster-town-a-dfylcjva.md)). Until step 3 ships, `POST /api/collectives` needs a human admin token, so the team can't create it. Without it the hosted checks (401 for a pasted token in a hosted World, 400 for a `workshop` slug, 409 for a duplicate) are skipped.
2. **One real GitHub sign-in** (outbox [dc_3oslgrfo6j](../../../../../town-hall/outbox/2026-10/2026-10-27-sign-in-once-on-muster-town-and-confirm-your-role-slgrfo6j.md), 5 minutes): sign in once, open /demo/ (no second GitHub prompt expected), check /demo/api/me says admin and /api/me still shows your Workshop role. The team has no never-granted GitHub account, so only you can do this.

## Borderline decisions
- Approved Tae's plan to put `POST /api/collectives` on the interact allowlist (a never-granted stranger can create) with a hard cap of one active collective per GitHub id and no cap for town admins, and to let `safeReturnTo` accept `/` so a signed-out visitor returns to the homepage form. Say if you want a different cap.
- Known limit, not a step 3 goal: hosted Worlds run with no agent runtime (main.ts:59), so a hosted collective's agents will not run even with a key. Step 3 ships the key store and the hold state; its report will say exactly what remains for agents to run, and that becomes the next step or a new grant.

## Key results
- kr_7316be4jqw (hosted collectives) on gr_rdyrjzclfe: 458,689 / 1,000,000 tokens; steps 1 and 2 live, step 3 (≤300 k) starts after the deploy, step 4 (live check with a second account, manual, README, ≤100 k) after that. Status: not-started → on course for claimed within the grant if steps 3–4 land at budget.
- Other KRs: no change. KR 6 staleness sweep 2 runs tomorrow ~06Z (Craig, exploration, ≤100 k).
- Spend today by lane: exploration 150,574 / 828,571 tokens; directed 612,394 tokens.
