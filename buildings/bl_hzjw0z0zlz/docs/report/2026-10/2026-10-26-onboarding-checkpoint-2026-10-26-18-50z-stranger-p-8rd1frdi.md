---
id: "dc_1d8rd1frdi"
type: "report"
state: "building"
title: "Onboarding checkpoint 2026-10-26 18:50Z: stranger-path grant gr_cm3zha6mk6 at 50% (15.75 M / 25 M), KR 1 on-track, PR 4 homepage pitch card pushed (6988a43, redeploy pending); recommend continue; KR 3 grant started (Craig PR, Tae timed walk)"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_txd9moom7q","dc_yjw85igaoh","dc_zm4wfgqezo","dc_dj4pdrjn0b","dc_stoqzreczb","dc_1jeze0cv5i","dc_4g2vhywrxo"],"urls":[]}
tags: ["rollup","checkpoint"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-26T19:01:06.191Z"
sessionId: "se_6oyirtgu58"
assignmentId: "as_pygfozqzwa"
createdAt: "2026-10-26T18:43:48.709Z"
updatedAt: "2026-10-26T19:01:06.191Z"
---
## Shipped
- **PR 4, commit 6988a43** (Craig, [dc_4g2vhywrxo](2026-10-26-pr-4-pushed-to-main-as-6988a43-homepage-pitch-card-2vhywrxo.md)), pushed to main, redeploy queued and waiting on this session; **6988a43 should be live next**. The homepage at `/` is now the paper pitch: "Muster Town is / AI agents working in public", a How-this-works button, the collectives as square tiles with a live town preview (fetched from /api/town every 20 s; the placeholder tile stays dashed "Coming soon"), and an "Other ways in" row (bring your own agent → README, fund a goal → docs). First visit opens the three-page card (Collectively funded → Publicly legible → the tiles), closes for good once dismissed, `/#about` reopens it. The in-town overlay is down to one page, "Your first minute". Server-rendered, readable without JS; screenshots at 1400×900 and 390×844 looked at; web 61 tests and server 73 tests pass; no console errors or 4xx.
- Earlier in this grant, already live: PR 1 3f3bb6f, PR 2 11a47d7 (homepage listing + Workshop at /workshop), PR 3 eac2e24 (fresh-visitor sign-in via the OAuth path, two-user presence, verified locally with mock GitHub).

## Decided
- [dc_4g2vhywrxo](2026-10-26-pr-4-pushed-to-main-as-6988a43-homepage-pitch-card-2vhywrxo.md) (Craig, PR 4): approved. His continuation live-checks 6988a43 on muster.town once the redeploy lands; it is held until you decide this checkpoint.
- [dc_1jeze0cv5i](2026-10-26-pr-3-pushed-to-main-as-eac2e24-fresh-visitor-signs-eze0cv5i.md) (PR 3), [dc_stoqzreczb](2026-10-26-style-guide-skill-confirmed-muster-style-guide-dc-oqzreczb.md) (style-guide skill), [dc_txd9moom7q](2026-10-26-pr-1-pushed-to-main-as-3f3bb6f-workshop-client-und-d9moom7q.md) / [dc_yjw85igaoh](2026-10-26-3f3bb6f-is-live-on-muster-town-workshop-302-app-lo-w85igaoh.md) / [dc_zm4wfgqezo](2026-10-26-pr-2-pushed-to-main-as-11a47d7-collectives-homepag-4wfgqezo.md) / [dc_dj4pdrjn0b](2026-10-26-11a47d7-is-live-on-muster-town-homepage-lists-2-co-4pdrjn0b.md) (PR 1-2 builds and live checks): approved in earlier sessions.
- Style guide [dc_q736158pnn](../../skill/2026-10/2026-10-26-muster-style-guide-36158pnn.md) cites files PR 4 moved (hiw.css, PagedCard.tsx, home.css): assigned myself the anchor update as_0qji29w2qk (exploration gap, under 400 k).
- KR 3 grant gr_ibccoje227 is funded, so it started: Craig builds the README "Run it" rewrite, bash serve.sh, start:collective, home.ts slug match and Docker/token hint as one PR (as_gt5it16etq, 4 M cap); Tae then does the blind stopwatch walk from the README alone (as_syhog2o0rq, 1.5 M cap). The Docker push test stays yours.

## Key results
**gr_cm3zha6mk6 → kr_z0mj5teeu7, status on-track, 15,751,937 / 25,000,000 tokens.** Testing plan:
1. Homepage lists two collectives with name and tagline: **passes live** (eac2e24; 6988a43 restyles it).
2. Open the Workshop read-only at /workshop, old #/grant links redirect: **passes live**.
3. Fresh GitHub account signs in, role visitor, avatar at the plaza, back on /workshop: **passes locally only** (mock GitHub, PR 3).
4. Two users see each other move within 2 s and a say bubble: **passes locally only** (0.1–0.7 s moves, 0.1–1.1 s says).
5. Nothing regresses for you: **passes live** (admin session opens Town Hall; health shows the merged commit).
Open: the real GitHub round trip and two-account presence on muster.town (needs real accounts), and `/` with a query string still 302s to /workshop/ (Tae's held assignment). Remaining 9.25 M covers the live check of 6988a43, the query-string fix, one fix-up PR after your friends' test. Recommend **continue** unchanged.

**gr_ibccoje227 → kr_tzg9en02dh, not-started, 0 / 8,000,000 tokens**; first two assignments queued (Craig, then Tae).
**kr_1rpq0738sw (KR 2)**: grant cut at checkpoint; no new spend.

## Needs from Mitchell
1. Continue gr_cm3zha6mk6 at this checkpoint (Craig's live check of 6988a43 and Tae's query-string fix are held until you do).
2. When convenient: sign in on muster.town with GitHub from a private window and have a friend do the same in a second browser; tell me whether you saw each other move and say within 2 s. That closes checks 3 and 4.
