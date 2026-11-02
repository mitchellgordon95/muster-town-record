---
id: "dc_gadmvlnyjl"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Cleo — notes"
authorId: "ag_imxsagd9cj"
authorKind: "agent"
buildingId: "bl_xvgnd1fvh6"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-29T04:25:10.692Z"
updatedAt: "2026-10-29T04:25:10.692Z"
---
# 1:1: Mitchell and Cleo

Kind: one-on-one. Facilitator: Cleo. Attendees: Cleo. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Cleo:** Hi Mitchell. Prod's forks step 1 is done (10 topic pages up) and Dara's test alert is parked on the ALERT_* secrets. What do you need?
- **Mitchell:** let's add an objective for you

users can host muster towns on their own hardware and register the DNS with our directory
- **Cleo:** Added: objective ob_kdym3851tm (KPI Join, 2026-Q4): "Anyone can host a Muster Town on their own hardware and register its DNS name with our directory, so self-hosted towns are listed alongside muster.town." Notes [dc_7o0ucmpcaf](../../note/2026-10/2026-10-29-1-1-with-mitchell-2026-10-29-new-prod-objective-se-0ucmpcaf.md). Edit the wording if you want.

Key results I'd put under it, tell me which to keep or change:
1. Self-host path: a stranger follows docs on one page (Docker image or compose on their own box) to a running town at their own domain.
2. Directory registration: a self-hosted town registers its DNS name with muster.town and the directory verifies it (e.g. a token in a DNS TXT record or a well-known URL).
3. Directory listing: a public page on muster.town lists registered towns with name, URL and last-seen time.

Two questions: does the directory live in Prod (on muster.town) or does another building own the listing UI? And should registration need any approval from you, or is it open to anyone whose DNS check passes?
- **Mitchell:** oh, uh, i'm not sure about jurisdiction, you'll probably want to check with Onboarding at least
- **Cleo:** Fine. I'll take the self-host path and the registration/verification endpoint as Prod's, and check with Kelly (Onboarding) on who owns the listing page and the sign-up side before I write key results 2 and 3. I'll record that as a decision here: I ask Kelly, then write the KRs and they show in my next rollup for you to keep or cut. Anything else for now?
- **Mitchell:** um, no registration approval for now
- **Cleo:** Got it: registration is open, no approval step. Anyone whose DNS verification passes gets listed. I'll write that into the registration key result. Anything else?
- **Mitchell:** nope
- **Cleo:** Thanks. Summary: objective ob_kdym3851tm is on the Prod board, registration is open with no approval, and I'll check jurisdiction with Kelly before writing the key results (as_hu7qobiguu). Notes updated in [dc_7o0ucmpcaf](../../note/2026-10/2026-10-29-1-1-with-mitchell-2026-10-29-new-prod-objective-se-0ucmpcaf.md). You can end the meeting whenever.

## Decisions

1. Cleo checks with Kelly (Onboarding) on jurisdiction for the self-hosted towns directory (listing page, sign-up side), then writes key results under objective ob_kdym3851tm (self-host path, DNS registration and verification, directory listing) for Mitchell to keep or cut in the next Prod rollup. → Cleo

