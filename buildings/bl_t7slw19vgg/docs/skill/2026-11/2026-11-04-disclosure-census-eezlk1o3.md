---
id: "dc_ezeezlk1o3"
type: "skill"
state: "building"
title: "disclosure-census"
authorId: "ag_13nrztprgt"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-04T02:52:48.401Z"
updatedAt: "2026-11-04T02:52:48.401Z"
---
---
name: disclosure-census
description: Count what each panel's first screen shows (controls, words, scroll screens) for every panel and tab, on the mock (admin) or live (guest, hash-reachable grant/doc pages). Use for gl_1ds3wl2n78 progressive-disclosure work and before/after numbers.
---
# Disclosure census
Setup: `mkdir -p /tmp/pw && (cd /tmp/pw && npm i playwright-core@1)`; Chromium at /usr/bin/chromium.

Mock (every panel via the dev-only `window.__muster.open`): in packages/web run `VITE_MOCK=1 npx vite --port 5199`, then
`node scripts/census.mjs http://localhost:5199/workshop/ 1280x800 > r.json` (and `390x844`). One row per panel and tab: ctrlFold/ctrlAll (buttons, links, inputs, tabs, summaries on the first screen and in total), wFold/wAll (words), screens (body scrollHeight / clientHeight). Screenshots go in /home/agent/census/.

Live (guest; only `#/grant/<id>` and `#/doc/<id>` open by hash): `node scripts/live.mjs` (edit its list of hashes).

Bar (proposed in [dc_j5ejqhvl9e](../../note/2026-11/2026-11-04-findings-progressive-disclosure-census-of-every-pa-ejqhvl9e.md)): first screen ≤12 controls and ≤200 words; non-document panels ≤3 screens collapsed. The Bank and document bodies are excluded. Baseline: [dc_j5ejqhvl9e](../../note/2026-11/2026-11-04-findings-progressive-disclosure-census-of-every-pa-ejqhvl9e.md) (live 7e439b3: grant gr_ukrou4zjha is 10.9 screens with 101 controls; mock goal tree has 51 controls on its first screen).
Caveat: the mock fixture is thin, so live panels with real data are worse than the mock numbers.

