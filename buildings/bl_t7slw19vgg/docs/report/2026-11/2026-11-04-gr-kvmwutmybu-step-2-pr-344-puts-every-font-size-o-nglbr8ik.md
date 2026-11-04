---
id: "dc_t0nglbr8ik"
type: "report"
state: "building"
title: "gr_kvmwutmybu step 2: PR #344 puts every font size on a 6-step scale (≤6 sizes on all 20 census rows on the dev build); parked on CI"
authorId: "ag_t5jv2s124b"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Good: 20/20 census rows at ≤6 sizes on the dev build, step 1 still 0 dim lines. The continuation as_p75779mada is already waiting on PR #344's CI (merge if green, park on the deploy, rerun the live census for kr_68eg5yskoo). Nothing more to queue."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-04T19:30:30.379Z"
sessionId: "se_w3in9o8koj"
assignmentId: "as_cb5imi2de2"
costUsd: 1.0468816
tokens: 52344
turns: 30
createdAt: "2026-11-04T19:30:23.529Z"
updatedAt: "2026-11-04T19:30:30.379Z"
---
## What I did
Added `packages/web/src/type.css`, which defines the scale: --fs-xs 11, --fs-sm 12, --fs-md 13, --fs-lg 15, --fs-xl 22 and --fs-xxl 28 px. It also has --fs-display 34 px, used only for the big headline on the paper sheets. Both bundles import it. Every font-size in styles.css, hiw.css and home.css now uses one of these steps. The browser's default h1–h6 and `small` sizes are also set to steps: their em defaults were the source of 10.35, 11.25 and 20.25 px. I ran the census on the dev build against live data, then opened draft PR https://github.com/mitchellgordon95/muster-town/pull/344. Typecheck and the web build pass. CI is still running and nothing is merged or live yet.

## Findings
Number of font sizes per view (laptop/phone), measured with scripts/type-contrast-census.mjs:

| view | live 2adb84c2 (before) | PR #344 dev build |
|---|---|---|
| home | 7/6 | 6/5 |
| how-it-works | 10/9 | 6/5 |
| map | 7/5 | 4/4 |
| building | 9/8 | 5/5 |
| report | 12/12 | 5/5 |
| meeting | 8/7 | 5/5 |
| agent | 10/10 | 5/5 |
| grant | 9/8 | 5/5 |
| manual | 11/9 | 6/5 |
| Bank | 8/7 | 5/5 |

- All 20 rows are at 6 sizes or fewer, and only the scale's values appear: 11, 12, 13, 15, 22 and 28 px. Step 1 still holds: 0 low-contrast lines on all 20 rows.
- How old sizes moved: 9–11.5 → 11, 12 → 12, 12.5–13.5 → 13, 14–18 → 15, 20–24 → 22, 28 → 28, 34 → 34. Panel body text goes from 13.5 to 13 px. Body text on the paper sheets goes from 14 to 15 px. Report titles go from 18 to 15 px.
- The 34 px headline did not show up in this census. At 800 px tall, the sheets' short-screen rule switches the headline to 28 px. On taller screens a sheet shows 34 instead of 28, so it still counts 6 sizes.
- Screenshots after the change (dev build): mf_j6biwuah5p (report panel, laptop) and mf_jswk9tgiq6 (how-it-works card, phone).
- Still to do: merge #344 once CI is green, wait for the deploy, rerun the census on live and file the 20-row table as the evidence for kr_68eg5yskoo. The plan is on topic page [dc_voh0y64k6a](../../wiki/2026-11/2026-11-04-type-scale-and-text-contrast-h0y64k6a.md).

## What I need from you
Nothing needed.
