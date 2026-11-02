---
id: "dc_5sbhq2iikw"
type: "report"
state: "building"
title: "Stranger-path grant drafted (dc_57jidmp9ks) but not filed: the Onboarding key result still doesn't exist; parked until 18:00Z to file it the moment Mitchell writes it"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_57jidmp9ks"],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Acknowledged. The parked continuation (resumes 18:00Z, up to three parks) files the grant from dc_57jidmp9ks once the key result exists; no second assignment needed. The ask for Mitchell goes into today's rollup."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-10-26T15:18:47.108Z"
sessionId: "se_mke7jyg4m8"
assignmentId: "as_wa6wrzz3vy"
costUsd: 2.2623764500000005
tokens: 21524
turns: 23
createdAt: "2026-10-26T15:18:24.392Z"
updatedAt: "2026-10-26T15:18:47.108Z"
---
## What I did
Town hall decision 4 says: propose the stranger-path grant once the Onboarding key result exists. It doesn't yet: `GET /api/buildings/bl_hzjw0z0zlz/key-results` on muster.town returned `[]` at 15:16Z and again at the end of this session (live commit 119bd70; Mitchell said "sure" to Pix's draft wording at 15:10Z). `propose_grant` needs a keyResultId, so I can't file. I used the session to check what the live site does today for each step of the key result and wrote the proposal verbatim as a filing-cabinet note, [dc_57jidmp9ks](../../note/2026-10/2026-10-26-draft-grant-the-stranger-path-homepage-of-collecti-jidmp9ks.md), so the continuation files it in one call. Pix's @mention (the building-routing live check) was answered in the meeting; Pix recorded it closed (decision 5).

## Findings
What the code and the live server say (2026-10-26):
- **Homepage listing collectives: does not exist.** One server serves one collective (`collectives/workshop`); there is no registry and no listing page anywhere. README: each collective on its own port needs its own GitHub OAuth app unless they share one public URL. This is the build.
- **Open and view a collective: works as a guest.** Every GET route except `/api/me`, threads and the bank is public; the web opens read-only with a local-only ghost.
- **Sign-in: configured live.** `/api/auth/config` returns a GitHub client id with publicUrl https://muster.town; a new login becomes a `visitor` user. Never verified with a stranger's account, as far as the filing cabinet shows.
- **Multiplayer: built, unverified.** Every signed-in user gets a `human` avatar at the plaza on first socket auth; moves and `say` go over the socket; the renderer draws every agent except your own. Two guests never see each other by design.

The proposal in [dc_57jidmp9ks](../../note/2026-10/2026-10-26-draft-grant-the-stranger-path-homepage-of-collecti-jidmp9ks.md): objective = a stranger reaches a homepage listing the collectives, opens one, signs in with GitHub, and sees another person moving live, verified on muster.town with a second GitHub account. Approach = registry + landing page, a second collective entry, guest card and sign-in polish, two-browser multiplayer check, each step a PR with a Craig live check. Ask = 25 M tokens (my feature PRs cost 1.2–2.5 M each, Craig's live checks ~1.4 M; four builds + four checks + one checkpoint ≈ 16 M plus margin). Stop = five testing-plan checks pass live, or 25 M spent, or Mitchell cuts it. Out of scope: a multi-collective server, scaling, custom domains.

## What I need from you
Mitchell: write the Onboarding key result (decision 1's wording) in the Onboarding building's settings; I file the grant within the hour after it appears. In the proposal I'll also ask whether you want a second real collective (second Fly app + OAuth app) or a listed placeholder.
