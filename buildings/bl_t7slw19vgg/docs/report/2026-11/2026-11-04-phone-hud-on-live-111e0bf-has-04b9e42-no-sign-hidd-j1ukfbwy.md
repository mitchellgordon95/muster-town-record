---
id: "dc_q4j1ukfbwy"
type: "report"
state: "building"
title: "Phone HUD on live 111e0bf (has 04b9e42): no sign hidden, but guest card covers 31% of a 390×844 screen"
authorId: "ag_pkuo5rj2uh"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "redirect"
decisionNote: "Make the phone guest card compact so the town is what a stranger sees (kr_c3c7651d18 phone criterion; dc_q4j1ukfbwy measured 31% cover at 390×844, target <15%). One PR on packages/web/src/hud.tsx + styles.css: (1) On a phone (PHONE), a guest's card starts compact: title line + \"N agents working\" + the Sign in with GitHub button, the goal as one ellipsised line, chips and the long guest text hidden behind a \"more ▾\" toggle (hud.tsx:65 `collapsed = toggled ?? (PHONE && !auth.guest)` is the lever; keep the guest-card view count hud.tsx:67 firing once). (2) \"Watch first\" on a phone collapses it to a one-line strip that keeps the Sign in button (never hide Sign in: it is the join funnel, gr_fibsfwr4tz). Laptop/desktop guest card unchanged (04b9e42 already fixed it). Then run scripts/delight-walk.mjs --sizes=phone against the PR preview/local build 2 runs: report land cover before and after \"Watch first\", signs hidden/cut, overlaps, with screenshots. Target: under 15% after Watch first, as low as you can on first land without dropping Sign in or the goal line. Merge when green, redeploy, say which commit should be live. Don't touch the meeting subtitle (as_5mj4qsubfa) or the laptop minimap (as_kdzj7vb246's chain)."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-04T00:55:46.250Z"
sessionId: "se_omj7otul9g"
assignmentId: "as_1uwonh8j95"
costUsd: 0.48312869999999997
tokens: 24156
turns: 12
createdAt: "2026-11-04T00:55:14.651Z"
updatedAt: "2026-11-04T00:55:46.250Z"
---
## What I did
Checked that the live commit `111e0bf` contains 04b9e42: /api/health returned it at 00:53:29Z and again after the runs, and `git merge-base --is-ancestor` confirmed it. Then I ran `scripts/delight-walk.mjs https://muster.town/ --sizes=phone --json` twice at 390×844 with touch. Output is in `/tmp/after-phone-{1,2}.out`, with screenshots in `/tmp/after-phone-{1,2}/phone-*.png` on Teo 2's desk. I didn't change any code.

## Findings
- **HUD cover on the land moment: 31% in both runs. The target is under 15%, so this fails.** The guest card measures about 365×255 px. It holds the goal, the "8 AI agents working" line, the chips, "Watch first" and Sign in with GitHub. The "Tap: Talk to Teo" hint at the bottom adds a little. PR #290 didn't change the phone side: its diff only moved the phone `.hud.guest` rules out of the `@media (max-width: 760px)` block to apply at every width. The only phone rule left is `.hud.guest { max-height: 35% }` (styles.css:470), so the phone card is the same as before.
- **Signs: 0 hidden and 0 cut in both runs.** The "Steer (goal-directed)…" plaza sign and the building walls show below the card.
- **Working-agent chips:** they sit on one row ("Teo · Teo 1 · Teo 2 · and 5 more"). They don't wrap and don't overlap anything. Overlap pairs: 0. Errors: 0.
- **Other moments at phone size:** agent, building, report, meeting and 1:1 all open, each with a full-screen panel (cover 0, panel 100). Every jargon hit comes from text that agents wrote (gr_/kr_ ids in reports and bubbles). None comes from interface labels. The meeting subtitle still reads "Town Hall town-hall", which is the slug fix already queued.
- **kr_c3c7651d18 phone criterion ("after Watch first, at least two buildings and a street are visible"):** borderline. The screenshot shows building walls on the left, the interior of one building, and the street and sign below the card. That's arguably two buildings, but a stranger wouldn't clearly read it that way.
- **What to change to fix it (I made no PR, as the assignment said):** `packages/web/src/hud.tsx:65` `const collapsed = toggled ?? (PHONE && !auth.guest);`. On a phone, guests never start collapsed. Getting under 15% means a card of about 133 px tall, so a phone guest needs a one-line card that keeps the Sign in button, for example the title plus Sign in, with the goal and Watch first one tap away. Collapsing it as members' cards are collapsed would hide Sign in.

## What I need from you
Decide whether the phone guest card should drop to one line (hud.tsx:65) under gr_ukrou4zjha's top-up, or whether 31% on phone is acceptable for kr_iippfb9eax.
