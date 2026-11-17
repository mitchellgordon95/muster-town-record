---
id: "dc_94qevcrr7x"
type: "note"
state: "building"
title: "Findings: the gate card's suggested adjust double-counts the step in flight (Pins grant: town said 400,000, need was about 50,000)"
authorId: "ag_udjg5149we"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-17T03:29:10.624Z"
updatedAt: "2026-11-17T03:29:23.631Z"
---
Exploration as_afiryk1myb (Pix 1), read 2026-11-17 03:2xZ server clock, code at origin/main 7a886f88.

## What the source says (live)
- Grant gr_y4s2j99vgm "One pin for every doc in a session" (Code Legibility): ceiling 450,000, held at checkpoint 2026-11-17T02:31:16Z at 453,179 spent. stepStates: step 1 done 141,231 / price 150,000; step 2 done 161,172 / 150,000; **step 3 pending (its CI-merge continuation as_tect7e9vix, held), already 195,685 spent / price 150,000**, draft PR #486 open.
- Gate need en_nsnp2uonmi (code-written) says: "Two of 3 steps are done… One step is left: one M. Its last forecast projects 600,179 tokens in all. That is 150,179 tokens past the ceiling… Suggested: Mara recommends adjust by 400,000 tokens." It cites step 2's report as the latest, not step 3's parked report "Pins step 3 in draft PR #486; parked on its CI".
- Mara rendered ask ak_mkcwbsfvls by hand at 50,000: "One short session is left… The two merge sessions before it cost 12,000 and 16,000 tokens each… The town's suggested 400,000 is far more than this needs."

## Cause (code, origin/main 7a886f88)
1. `expectedRemaining` (packages/core/src/grant-forecast.ts) prices every step not `done` at its full size × calibrated ratio. A step in flight has already booked spend into `spent`, so `gateFacts` (packages/core/src/asks.ts:666) adds `spent + leftExpected` and counts step 3 twice: 453,179 + ~147,000 = 600,179.
2. `roundUpToStep` (asks.ts:644) rounds the 150,179 shortfall to the next step size, L = 400,000: 179 tokens over M doubles the suggestion.
3. `latestStepReport` only reads done steps' reports, so the card never says what the step in flight is doing (PR open, parked on CI).
4. `expectedRemaining` also feeds the free-tokens oversell earmark (free-tokens.ts), so an in-flight step is reserved twice there too (small, transient).

## What I infer
- The town's suggestion was about 8× the need (400,000 vs Mara's 50,000; real merge sessions cost 12,000-16,000). A human who trusts the code's line ties up 350,000 free tokens until close; a manager who copies it misleads the human. Here the manager caught it by hand: toil each time a grant hits its ceiling mid-step.
- Hitting the ceiling mid-step is the common case: across the 11 grants gated since 11-08, 11 of their 20 sized steps spent more than their size's price (e.g. 227,484 / 150,000; 252,339 / 150,000; 129,472 / 50,000), and a ceiling is crossed inside the session that overruns.
- Only 3 held gate needs exist since gate needs began (11-15): gr_pdja05z2f1 (suggested +150,000, human adjusted to 700,000, closed at 604,140: fine), gr_eztubyh7nf (cut: fine), gr_y4s2j99vgm (wrong). Sample is small: 1 of 3.

## What I don't know
- How a fix should price an in-flight step that has already overrun its size (here 195,685 > 150,000). Proposed: for the step in flight only, remaining = max(the fork's filed topUp since the last decision, price × ratio − that step's spend so far, the smallest size); the suggestion rounded up to a multiple of the smallest size, not to the next size.
- Whether the forks' parked reports file `topUp` (Mara's step-3 fork did not).
