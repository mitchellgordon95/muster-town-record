---
id: "dc_dy4dwf5jw5"
type: "report"
state: "building"
title: "Style guide skill dc_q736158pnn updated for the operating manual: new section 6 (manual paper sheet, routes, \"?\", slugs, library doc as source of truth), hue-hex rule settled (three hue pairs may be retyped for a title or status dot; next hiw.css PR lifts them to variables), references re-pinned to main 39a7906, which is live"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_qr00e8k1yk","dc_q736158pnn","dc_jrvx5amnj6"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Style guide covers the manual sheet; nothing further."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-10-27T05:15:34.385Z"
sessionId: "se_xk6beavexe"
assignmentId: "as_sbm4cwpx34"
costUsd: 3.3613537000000004
tokens: 39455
turns: 17
createdAt: "2026-10-27T05:14:43.790Z"
updatedAt: "2026-10-27T05:15:34.385Z"
---
## What I did

Read skill [dc_q736158pnn](../../skill/2026-10/2026-10-26-muster-style-guide-36158pnn.md), then the code on main at 39a7906 (which contains bb7c00f and is live on muster.town: `/api/health` commit 39a7906, `GET /api/manual` 200): panels/Manual.tsx, manualSections.ts, hiw.css, HowItWorks.tsx, hud.tsx, app.tsx, route.ts, state.ts, api.ts, mock/server.ts, test/manual.test.ts, docs/manual.md, plus home.css, home.ts, styles.css, PagedCard.tsx to re-check the existing references. Rewrote the skill with `write` (type skill, same id, state building). No code change, no PR. Wiki pages "Style guide" and "Operating manual" rewritten; log appended.

## Findings

- **New section 6, "The manual sheet"**: `.paper.manual` is the 760px sheet frame scrolling over the town (hiw.css:50-75), head kicker + green h2 + ×, TOC chips with the paper-button look, one `<section data-slug>` per h2 with an h3 that links to itself, a 12px note to the library doc; routes `#/manual[/<slug>]` (route.ts:9,24); Esc/focus/backdrop/hash-router behaviour (Manual.tsx:19-35); entry points HUD "?" (hud.tsx:117, app.tsx:245) and the overlay's last line (HowItWorks.tsx:27). Rule: it is the one non-paged paper modal; anything paged still uses PagedCard. Copy rules: h2 titles are noun phrases ≤ 4 words because they become chips and URLs (slugs pinned by test/manual.test.ts), insider words allowed but defined in bold on first use, and a copy change is live only on the library doc (the repo file seeds once).
- **Craig's bend of checklist 1 recorded and the rule set**: `.manual-head h2` retypes green #2f7d46 and `.manual-body h3` blue #2d6aa8 (hiw.css:54,67), as home.css:9 and :22 already did, because the hues live on `.hiw-page` and `.paper` can't read `--hue`. Going forward (section 2, Don't, checklist 1): a sheet's title is green, section headings blue, status dots green; those three hue hexes are the only retype allowed outside hiw.css:12-14, and only for a title or a status dot. The next PR that touches hiw.css lifts the three pairs onto `.hiw, .paper` as `--green`/`--blue`/`--amber` (+ `-bg`), points `.hiw-page` at them and switches the four sites; after that retyping is a bend again.
- **Drifted references fixed** (the skill said main at 76c6ad1): styles.css breakpoints 390/393 and `.help-btn` 512-513, hud.tsx guest card 143 and touch hint 207, home.ts kicker/button/ways/foot 89-103, app.ts:116, PagedCard foot 46-55; section 5 now says the "?" opens the manual, not the overlay, so the overlay shows once per browser with no in-town reopen. Sections renumbered 6→7 … 11→12 with cross-references updated.
- Length: ≈118 lines, up from ≈96 (within the +25 asked). Description trimmed to 300 chars (the tool's limit).
- Side observation: bb7c00f is already live, so Craig's parked technical check and Tae's as_gn9cdj8ma7 should be running or about to.

## What I need from you

Nothing needed.
