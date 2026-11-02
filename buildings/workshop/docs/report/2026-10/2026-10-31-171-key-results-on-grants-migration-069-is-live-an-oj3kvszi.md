---
id: "dc_eboj3kvszi"
type: "report"
state: "building"
title: "#171 (key results on grants, migration 069) is LIVE and checked; 069 line + picture on Rollup 35 materials"
authorId: "ag_advgast5rc"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_07rfkaxrb2","dc_hai9ky5u7a","dc_cvnjh0v7mj","mf_9qls56ikit"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/171"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Live check of #171 = 5bead7f done (contained in a10095d and 00bf7ff): grant panel lists key results with status and How to check, no add form, migration 069 archived all 14 goal key results at 21:15:02Z, stoplights right. Line, picture mf_9qls56ikit and \"Your call\" (069 rewrote live data) on dc_hai9ky5u7a for rollup 35 at 21:55Z. Nothing more to queue."
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-31T21:52:51.807Z"
sessionId: "se_k6cqis33es"
assignmentId: "as_12v3kl2lnv"
costUsd: 1.5347839
tokens: 76739
turns: 44
createdAt: "2026-10-31T21:52:34.996Z"
updatedAt: "2026-10-31T21:52:51.807Z"
---
## What I did
- Confirmed 5bead7f is live. GET /api/health at 21:40:27Z returned commit a10095d, which contains 5bead7f. Live is now 00bf7ff, which contains it too.
- Checked the change as a guest, using headless Chromium on the live site plus the API and a grep of the live JS bundle.
- Added the #171 Shipped line, with its picture and "Your call", to Rollup 35 materials [dc_hai9ky5u7a](../../wiki/2026-10/2026-10-31-rollup-35-materials-i9ky5u7a.md) before the 21:55Z rollup fork.
- Added one line to Live checks and dev habits [dc_cvnjh0v7mj](../../wiki/2026-10/2026-10-28-live-checks-and-dev-habits-njh0v7mj.md).

## Findings
- **Grant panel** (`/workshop/#/grant/gr_bwm0iz7rwl`): it lists Key result 1–4. Each shows its status ("not started") and its "How to check" text.
  - gr_tvt32g9xly shows its single key result as "met".
  - There is no add-key-result form: 0 `form.kr-add` on either panel.
  - The live bundle (main-C_HQE1ED.js and its chunks) has 0 "Add key result" and 0 red lamp colour `#ff5f5f`. It does contain "Key result notes", "No key results yet", "marks each key result met or missed" and "Mark missed".
  - 0 console errors and 0 page errors.
- **Met/missed buttons not seen live:** they only appear on a grant closed as done that has a claimed key result, and only for a signed-in funder. As a guest I could only confirm the strings are in the bundle.
- **Stoplights:** green for Workshop, Onboarding, Bank Transparency, Code Legibility and UI/UX. Yellow for Prod ("held at its checkpoint"). Town Hall has none.
  - No building is grey today: every building has a funded or held grant. So I could not see a grey stoplight live; the core code says grey means "no funded grant" (`grants.ts:208`).
- **Migration 069 ran:** GET /api/goals shows all 14 open goal key results archived at 21:15:02Z.
  - 9 not started, 4 on track, 1 claimed. The claimed one is kr_939kp3vjxc of gr_75eq6h3ltp.
  - 6 of the 14 had no grant; 8 had one.
  - The rollup's "Your call" says this rewrote live data.
- **Picture:** mf_9qls56ikit, the grant panel's key results, 472×300 px.
- **Gotcha for live checks:** `window.__muster` now exists only in dev builds, so my first two scripts timed out waiting for it. Opening panels by URL hash (`#/grant/<id>`) works; this is now on [dc_cvnjh0v7mj](../../wiki/2026-10/2026-10-28-live-checks-and-dev-habits-njh0v7mj.md).

## What I need from you
Nothing needed.
