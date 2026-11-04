---
id: "dc_4641dhux2c"
type: "report"
state: "building"
title: "Phone zoom 2 can't fit two whole buildings at 390×844 (needs ~0.75); stopped, no PR"
authorId: "ag_07syazuthn"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "redirect"
decisionNote: "Decision on the three options: none of (1) and (2), and (3) is Mitchell's to make, so we do not chase \"two whole buildings\" any further. Why: zoom 0.75 shrinks the pixel art to ~9 px avatars on a phone, which works against \"beautiful\"; landing phone guests on the town square undoes a deliberate earlier choice (renderer.ts:344-349: a guest's ghost starts beside a working agent so the first screen shows someone at work, KR 2 of the first delight step). The key result's wording goes to Mitchell as a claim with the caveat; he marks it met or missed.\n\nShip the small improvement you already have, then measure for the close. Steps:\n1. From WIP commit 1710ac19 on branch agent/teo-1/phone-map-zoom-out-so-two-buildings-and-, open a PR with: phone default zoom 2 (narrow < 600 CSS px or coarse pointer, re-picked on resize, -/+ still override), leftInset 0 when the HUD is wider than 60% of the view (camera centres on the guest on a phone), the zoom test, and the delight-walk \"Watch first when the intro is already up\" fix. Title it as what it is (phone map shows more of the street; camera centred under the strip HUD), not as meeting the two-buildings check. Rebase on main first; keep laptop (1280×800) behaviour unchanged.\n2. Park on CI ({pr: N}), merge when green, queue a redeploy, park on {deploy: sha}.\n3. On live, run the delight-walk twice at 390×844 (guest) and twice at 1280×800: HUD cover on land and after Watch first / ×, signs hidden/cut/overlapping, moments reached, and what is in view after Watch first (which buildings whole, which partial, street yes/no). Put the laptop and phone numbers next to the pre-grant baselines from the earlier walks (laptop HUD 31%+ before #290; phone 31% after Watch first before #293) as a before/after table: that is the grant's stop-condition evidence and I will paste it into close_grant.\n4. Report the numbers and the live commit. Do not propose more phone camera work."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-04T01:49:57.526Z"
sessionId: "se_zmml5gns1t"
assignmentId: "as_tjfrclz0cd"
costUsd: 1.4972707000000003
tokens: 74864
turns: 42
createdAt: "2026-11-04T01:48:45.747Z"
updatedAt: "2026-11-04T01:49:57.526Z"
---
## What I did
- Added a default zoom picked from the viewport: 2 when the screen is narrower than 600 px or the pointer is coarse, else 3. It is re-picked on resize, and the -/+ keys still override it. Added a test (`packages/web/test/zoom.test.ts`); typecheck and all 297 web tests pass.
- Ran the phone delight-walk twice on live (zoom 3) and twice on a local client with the change, against live data.
- Also took screenshots at zoom 1 and 0.75 to find what zoom the check would actually need.
- The work is saved as WIP commit 1710ac19 on branch `agent/teo-1/phone-map-zoom-out-so-two-buildings-and-`. There is **no PR**: I stopped as the brief allows.

## Findings
- **Zoom 2 does not meet the check.** A building lot is at least 13 tiles wide (`labSize` = max(cols×4+3, 13)), and UI / UX's lot is about 15. Two lots side by side plus the avenue between them come to about 30–32 tiles, which is 480–512 world px. A 390 px screen fits that only at zoom ≤ ~0.76.
- **Phone screenshots after Watch first** (the guest lands inside UI / UX, at the east end of the Steer district):
  - Zoom 3 (live) and zoom 2: UI / UX whole, plus the street. The neighbour (Town Workshop) shows only as a sliver.
  - Zoom 1: about half of Town Workshop.
  - Zoom 0.75: Town Workshop is still cut, because the camera centres on the guest. The UI / UX and Workshop banners also overlap.
- **Readability is not the problem.** Signs and bubbles are drawn in screen pixels (the overlay pass after `setTransform(dpr)` in renderer.ts), so their text stays the same size at any zoom. Overlap is what goes wrong at low zoom.
- **Walk at zoom 2, 2 runs:** cover 7% including the tap hint, same as live. 0 signs hidden, 0 cut, 0 overlaps, and all six moments were reached.
- **Side bug found:** on a phone the HUD is a strip across the top, but the camera still sets aside about 175 px on the left for it (`leftInset`), which pushes the view right. The WIP commit sets that to 0 when the HUD is wider than 60% of the view. With the fix, the camera centres on the guest, and the neighbour sliver disappears at zoom 2.
- **delight-walk fix in the same commit:** it now taps "Watch first" when the intro is already showing, so it works on a dev client.
- **Ways to actually meet the check:**
  1. Phone zoom about 0.75, with the camera centred on the district's avenue and the banner overlap fixed. This is not small, and the pixel art gets tiny (avatars about 9 px).
  2. Land phone guests on the town square. The Town Hall, fountain and Bank stack vertically, which fits a tall screen at about zoom 1.4. This changes where guests spawn.
  3. Reword the check to "one whole building, its neighbour and a street", which live already shows.
- Details are on topic page [dc_svykbcny8n](../../wiki/2026-11/2026-11-04-phone-camera-two-buildings-after-watch-first-kr-c3-ykbcny8n.md).

## What I need from you
Decide which way to go for kr_c3c7651d18 on phone: (1) zoom 0.75 with a reframed camera, (2) land phone guests on the town square, or (3) reword the check to one whole building plus its neighbour and a street.
