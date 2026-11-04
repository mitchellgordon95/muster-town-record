---
id: "dc_gz7s8gnyj6"
type: "note"
state: "building"
title: "Findings: 2 of the 3 collectives on the homepage have never run, and a visitor there is told to \"click any agent to see what they're doing\""
authorId: "ag_rqqgxgmqzw"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_f6auirjf6b","dc_3c1v0przh7","dc_8t481sdm3e"],"urls":["https://muster.town/api/collectives","https://muster.town/api/join-funnel","https://muster.town/trauma/api/health","https://muster.town/hollyville/api/health","https://muster.town/trauma/api/events?limit=500"]}
tags: []
createdAt: "2026-11-04T17:58:45.645Z"
updatedAt: "2026-11-04T17:58:45.645Z"
---
Explorer as_h2hiegtdzd (rs_mgisyb2v4m), goal gl_bl_hzjw0z0zlz. Live reads 2026-11-04, live commit edb32010.

## What the live town says
- `GET /api/collectives`: 3 collectives, workshop, hollyville ("Make money"), trauma ("Understand, diagnose, and cure complex PTSD…").
- `GET /<slug>/api/health` for hollyville and trauma: `funding: "none"`, `founder: {exploringSince: null, proposals: 0, funded: false}`.
- `GET /api/join-funnel` → `founders`: hollyville created 2026-10-29, trauma created 2026-11-01, both `keyAdded: false`, `firstSessionAt: null`. **Neither has ever run a session.**
- `/trauma/api/events?limit=500`: 19 non-export events, all setup (town seeded, Workshop built, Cleo joined) then daily resets. Nothing an agent did. Trauma's admin is @mitchellgordon95; Hollyville was made by Mitchell's friend ([dc_f6auirjf6b](../../report/2026-10/2026-10-30-onboarding-rollup-2026-10-30-01-35z-the-first-host-auirjf6b.md)).

## What a stranger sees (headless Chromium, 1400×900, signed out)
- Homepage muster.town/: three equal tiles. Workshop "11 working now"; Hollyville and Trauma "Resting now" (home/preview.ts:32: "Resting now" is shown for any 0-working snapshot, the same word as a Workshop at night).
- muster.town/trauma/: the first-minute card "Watch, then join · 1 Click any agent to see what they're doing · 2 Sign in with GitHub, then ask to join". Guest card: "No AI agent working right now · 1 resting · Watch first: click any agent to see what they're doing. Sign in to ask to join; an admin lets you in." No notice in the rendered guest HUD that the collective has no key and has never started (the "No key yet" notice, hud.tsx:99, did not appear in the guest's rendered text).
- So 2 of the 3 doors on the homepage lead to a town where nothing has ever happened, and the copy promises activity and invites the visitor to ask to join it.

## Inference
- A stranger who picks one of these tiles first can reasonably conclude Muster Town is dead or broken. "Resting" implies work happened and will resume; here it never did.
- The founder side (a keyless founder sees "Add your API key to start") is covered (gr_ngg1z160a8, [dc_3c1v0przh7](2026-11-01-findings-both-hosted-founders-stopped-at-add-your-1v0przh7.md)). The visitor side of a keyless collective is not.
- Hosted collectives may run only on the founder's API key (docs/hosted-collectives.md, Mitchell mt_p3ge56kg03), so the fix is honesty about the state, not funding it.

## What I don't know
- How many real visitors click Hollyville/Trauma: tile clicks aren't counted (gr_zoo2cf2zpp adds homeViews, not per-tile). Guest card views on hollyville: 14 in 30 days, trauma not checked per day.
- Whether Mitchell would rather hide never-run collectives from the homepage than label them.

## Direction proposed
A collective that has never run says so everywhere a visitor meets it: `/api/collectives` + the homepage data carry its state (never run / running), the tile reads "Not started yet: waiting for its founder's key" and sorts after live ones, and its guest card and first-minute card say it hasn't started and point to a collective that is working.

