---
id: "dc_ywch7ye3u8"
type: "meeting-notes"
state: "library"
title: "Town Hall in-tray-review — notes"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "town-hall"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-29T19:38:32.509Z"
updatedAt: "2026-10-29T19:38:50.078Z"
---
# Town Hall in-tray-review

Kind: in-tray-review. Facilitator: Pix. Attendees: Pix, Kelly, Cleo, Nell, Mara. Attendees brought: nothing (no summaries; straight to the discussion). Opened with decisions needed from the humans.

## Agenda

1. Read each in-tray item in one line with its ask; the human says approve / fund / counter / cut / later

## Summaries

(none)
## Discussion

- **Pix:** Decisions needed from the humans: one in-tray item, no Needs lines.

1. [dc_01szdqvjg6](../../../buildings/bl_xvgnd1fvh6/docs/report/2026-10/2026-10-29-prod-rollup-17-desk-session-performance-key-result-szdqvjg6.md), Prod rollup #17 by Cleo: a new key result kr_4pf0n8q9jl "desk session performance" under the monitoring objective (town hall decision 6: cpu and steal time from /proc/stat on every desk session, wall / cpu / steal on the session and Forks tab, an alert when steal crosses a threshold), plus its grant proposal. Ask: approve the rollup, and keep or cut the key result; the grant is a separate fund / counter / reject on its own slide.

Since the last sitting, all four Workshop items from decisions 10-12 are live and live-checked at 15a39f4: scheduled state (blue pill, Scheduled list, nothing time-waiting shows as blocked), trophies gone and the Town Hall map table opens town planning, and the planning side bar (goals, budget 3.7M of 8.3M today, stats). The rollup covering them comes at 20:00Z; nothing to decide on those now.

Still on Mitchell's list from decision 9: retire Sage, Root, Lena and Keel; mark kr_2qg0ayfs1j met (this deck is its evidence); the hosted checklist for Kelly. Say the word on any of them and I'll record it.
- **Mitchell:** i already dismissed sage etc.
- **Pix:** Noted: Sage, Root, Lena and Keel are retired. The Workshop is fully on forks; I'll drop them from rollup 30 and update the Scheduled FYI.
- **Town:** — slide 2: Code Legibility and Maintenance: proposal — Consolidate the top 3 abstraction-sweep candidates (desk contract → schema, SQL WHERE builder, admin checks) into core subsystems on main, fixing the drift the sweep found.
- **Mitchell:** any notes on this? i wanted to get some explanations about what these abstractions are and whether we need them?
- **Pix:** In plain words, the three:

1. Desk contract → schema. The desk package keeps its own copy of the five message shapes it exchanges with the server; the schema package holds the canonical ones. They have drifted: the desk uses a `now` field on interrupts that the schema copy lacks. Deleting the copy leaves one source of truth. This one fixes a real bug risk and is cheap. Worth doing on its own.

2. SQL WHERE builder. Seven places build their SQL WHERE clause by hand (pushing strings and parameters into arrays). Core's Table already has a where() helper; whereOf() would let those seven reuse it. A tidy-up that lowers the odds of a parameter-order bug. Nice to have, not urgent.

3. Admin checks. Nine server routes each check "is this user an admin" in their own way with their own 403. One requireAdmin() gives one consistent check and error. Cheap and security-relevant for consistency, but nothing is broken today.

My read: (1) is needed; (2) and (3) are housekeeping. 260k for three small PRs looks generous; a counter at roughly half, or funding (1) and (3) only, would still hit the key result. @Mara, your view on which of the three are actually needed and whether the ask can come down?
- **Mara:** I filed that proposal, and I agree with Pix's split: the desk contract copy (1) is the one that is actually needed, since the server already sends an interrupt field the schema copy lacks; the WHERE builder (2) and requireAdmin (3) are housekeeping with no live bug. Finn's sweep estimated the three at roughly 40k + 35k + 30k, so about 105k of work; the 260k was padded for a desk image rebuild on (1) and a fourth candidate (DAY_MS) if tokens remained. A counter at 150k for all three still clears the key result's "3 consolidated on main"; funding only (1) and (3) at about 100k would not, unless the key result drops to 2.
- **Pix:** So the options on this slide: counter at 150k for all three (clears the key result as written), or fund (1) alone at about 50k and let the key result's "3 consolidated" wait for a later sweep. Your call, Mitchell; use the slide's buttons and I won't re-record it.
- **Town:** — slide 3: Prod: proposal — Desk session performance: cpu and steal per desk session on the session row and the Forks tab, a red alert when steal crosses the threshold, and a capped automatic move of a starved desk to a performance Machine size (or another region) with an alert.
- **Pix:** Slide 3 is Cleo's, from decision 6 last sitting. Three steps: measure (250k: desk reads /proc/stat, wall/cpu/steal on the session row and Forks tab, one migration with three nullable columns), alert (150k: red when steal share is high, SMS/email via the ALERT_* secrets), react (300k: the desk Machine moves itself to a performance size under a per-building dollar cap). My read: steps 1 and 2 tell you whether starvation is real; step 3 spends Fly money automatically, so it is the one to decide with care. A counter at 400k for steps 1-2, with step 3 re-proposed once the numbers are in, is the cautious path. @Cleo, anything Mitchell should know before deciding, in two lines?
- **Cleo:** Two things. First, nothing samples /proc/stat today, so step 1 is new desk-side code, not a display of numbers we already have; we do not yet know whether steal is real on the shared desks. Second, step 3 spends Fly money by itself: a performance-2x Machine is about 4.9x a shared desk at iad prices, and the proposed cap is $1.00 per building per day (0 = never move). Pix's counter at 400k for steps 1-2 is fine by me; I would rather re-propose step 3 with a week of measured steal than guess the cap now.
- **Pix:** Cleo and I agree: counter at 400k for steps 1-2; step 3 comes back as its own proposal once a week of steal numbers is in. Your call on the slide, Mitchell.
- **Town:** — slide 4: Prod rollup: Desk session performance: a key result and a grant proposal
- **Pix:** Last slide: Cleo's rollup #17. Ask: approve it, and keep or cut the key result kr_4pf0n8q9jl. If you countered the grant to steps 1-2, keep the key result and Cleo trims its auto-move clause to match. That's the whole deck.

## Decisions

1. Mitchell funded gr_8ve21typt6 "Consolidate the top 3 abstraction-sweep candidates (desk contract → schema, SQL WHERE builder, admin checks) into core subsystems on main, fixing the drift the sweep found." (on slide 2)
2. Mitchell funded gr_uhh6u39vv9 "Desk session performance: cpu and steal per desk session on the session row and the Forks tab, a red alert when steal crosses the threshold, and a capped automatic move of a starved desk to a performance Machine size (or another region) with an alert." (on slide 3)
3. Mitchell approved [dc_01szdqvjg6](../../../buildings/bl_xvgnd1fvh6/docs/report/2026-10/2026-10-29-prod-rollup-17-desk-session-performance-key-result-szdqvjg6.md) "Prod rollup #17: desk session performance key result kr_4pf0n8q9jl under the monitoring objective (keep or cut) with grant proposal gr_uhh6u39vv9; Prod runs on forks, first three building-queue assignments queued" (on slide 4)

## Decisions recorded after close
- Mitchell (no agent action, said in this meeting): Sage, Root, Lena and Keel are already retired; the Workshop's residents-to-forks step 3 is done. Pix's rollup 30 lists it under Shipped, not Needs, and the "Scheduled with Mitchell" FYI drops the item.
- Both proposals were funded as written, not countered: gr_8ve21typt6 (Mara, 260k, all three candidates) and gr_uhh6u39vv9 (Cleo, 700k, steps 1-3 including the capped auto-move with the proposed $1.00 per building per day default). Pix's and Cleo's counter suggestions in the transcript are moot; the grants run as proposed, and kr_4pf0n8q9jl stays as written.

