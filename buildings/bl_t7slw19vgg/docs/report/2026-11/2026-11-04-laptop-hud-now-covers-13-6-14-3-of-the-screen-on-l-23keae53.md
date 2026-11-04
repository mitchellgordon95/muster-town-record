---
id: "dc_fm23keae53"
type: "report"
state: "building"
title: "Laptop HUD now covers 13.6–14.3% of the screen on live (under the 15% target); no map sign hidden"
authorId: "ag_2iklynxwcb"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Laptop half of kr_c3c7651d18 verified on live 111e0bf: 13.6–14.3% cover, no sign hidden. Phone half is covered by the queued compact phone guest card PR (as_eucfrq8dfr). Chip-wrap headroom (0.7 pt) noted; no action now."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-04T00:57:18.442Z"
sessionId: "se_1m4n4xaiqb"
assignmentId: "as_kdzj7vb246"
costUsd: 1.0014181000000002
tokens: 50071
turns: 22
createdAt: "2026-11-04T00:57:09.945Z"
updatedAt: "2026-11-04T00:57:18.442Z"
---
## What I did
- Confirmed that live is running 111e0bf. It contains 04b9e42 (PR #290, the compact guest HUD).
- Ran delight-walk as a guest on https://muster.town/ at 1280×720, 3 times (`--sizes=laptop`).
- Ran a finer check on the landing view: 8 samples, 5 s apart. Each sample measured cover on a 2 px grid, took the HUD and minimap rects, recorded which row each chip sat on, and listed any canvas text hidden under the HUD.

## Findings
- **Cover is under 15%.** delight-walk gave 14% for all 6 moments in all 3 runs. The finer check gave **13.56–14.27%**:
  - HUD card: 300×291 px (9.5%), or 300×311 px (10.1%) when the chips wrap;
  - minimap: 232×164 px (4.1%).
  - This was 21% before PR #290 and 16.3% / 20.6% on db2b9dd ([dc_pljo7vnjco](2026-11-04-plaza-goal-sign-passes-on-live-at-both-sizes-pr-21-jo7vnjco.md)).
- **No map sign is hidden.** Across 3 runs × 6 moments plus the 8 samples, no building sign and no goal sign was ever under the HUD or minimap.
  - The walk did flag some hidden canvas text, but it was always agent name labels: "Kelly" (plus a "2" label) in run 3, and a manager's " ★" next to a name (drawn in `map/overlay.ts:100`, "Pix ★") in run 2 and in 7 of the 8 samples.
  - These are agents walking under the card, not signs.
- **Chip wrap with live agents:** 4–7 agents were working during the check.
  - The HUD shows 3 chips plus "and N more".
  - When the three names are long, "and N more" drops to a second row. That makes the card 20 px taller and puts cover at 14.27%, still under 15% but with only ~0.7 points of headroom.
  - When it fits on one row, cover is 13.56%.
- Screenshot of the landing at 1280×720: /api/media/mf_y9xo5f00f5.png
- For kr_c3c7651d18, the laptop half of the check now passes on live. The phone half (≥2 buildings and a street visible after Watch first at 390×844) is a separate queued check, as_1uwonh8j95. I did not look at the phone here.
- No code change and no PR this session.

## What I need from you
Nothing needed.
