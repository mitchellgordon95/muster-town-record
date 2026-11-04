---
id: "dc_1tf1xefkbu"
type: "report"
state: "building"
title: "gr_kvmwutmybu step 4: PR #350, signed-in views 100/100 pass on the mock + manual Design section; parked on CI"
authorId: "ag_j7hkvaikti"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":["dc_voh0y64k6a","dc_aviiq4qxpa","dc_uzwcg5xw3u"],"urls":["https://github.com/mitchellgordon95/muster-town/pull/350"]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Acknowledged. PR #350 (signed-in views 100/100 on the mock, Design section in the manual) is parked on CI as as_49mgtd5x7v; that continuation merges, parks on the deploy, and reports the live evidence for kr_mmdday2x7z and kr_z4junko6nt. The grant is held at its checkpoint (dc_lp6e5f27gx), so the continuation runs once Mitchell continues it. Folds into the next rollup after the merge is live."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-04T20:54:52.899Z"
sessionId: "se_1mg5g080ya"
assignmentId: "as_p93ycyxkz1"
costUsd: 1.8457687
tokens: 92288
turns: 51
createdAt: "2026-11-04T20:54:44.324Z"
updatedAt: "2026-11-04T20:54:52.899Z"
---
## What I did
Added a mock mode to the type/contrast census that opens every signed-in panel and tab. I fixed the 8 failing rows and added a Design section to the manual. Then I opened draft PR https://github.com/mitchellgordon95/muster-town/pull/350 and parked it on its CI.

## Findings
- **Part A, kr_mmdday2x7z.** `MOCK=http://localhost:5199/workshop/ node scripts/type-contrast-census.mjs` covers every panel kind and tab on the mock as admin, plus the review deck, at 1280×800 and 390×844.
  - **Before (main aa6f4fbc):** 98 rows, all with ≤6 font sizes and 0 text under 11 px. 8 rows had low-contrast lines, all caused by `opacity` fades:
    - agent Assignments "done" rows: 2 lines, 4.12:1
    - meeting "no summary" cards: 2 lines, 3.32:1
    - goal tree "0 desks" tags: 7 lines at laptop, 5 and 3 at phone, 3.61:1
  - **Fix:** the opacity is gone. Those rows now step back with a transparent background or a dashed outline (3 CSS lines).
  - **After:** 100 of 100 rows have ≤6 sizes, 0 low-contrast lines and 0 text under 11 px.
- **Part B, kr_z4junko6nt.** `panels/DesignSection.tsx` is a section at the end of the manual, linked from its contents and at `#/manual/design`. It shows:
  - the 7 `--fs-*` steps with px and where each is used
  - the 24 colour tokens as swatches, grouped by role, with values read from the live CSS
  - a before/after contact sheet: mf_5ke5yff43d (live 0af4874 vs aa6f4fbc: agent Talk and Bank Donate tabs)
- **Two judgment calls in Part B:**
  - It is a React section, not markdown, because the live manual is a stored article seeded only once from docs/manual.md.
  - The type sample is an SVG picture. As page text, all 7 steps on one screen would break the ≤6-sizes bar. With the picture, the section measures 6 sizes at laptop and 5 at phone, with 0 low-contrast lines.
- **Checks:** `npm run check:css` finds 0 stray values. Typecheck passes and all 336 web tests pass.
- **Small error:** the commit message says "6 of 98" failing rows; the correct number is 8. The PR description has the correct figure.
- **Next session, after CI:**
  1. Mark the PR ready and merge it. Do not redeploy.
  2. Park on `{deploy: <merge sha>}`.
  3. Run the live census on the manual's Design view: `VIEWS=manual` plus the `#/manual/design` hash, at both sizes.
  4. Make one crop of the Design section, ≤300 px tall.
  5. Report evidence lines "Live <sha> (PR #350): …" so Teo can claim kr_mmdday2x7z and kr_z4junko6nt.

  The topic page [dc_voh0y64k6a](../../wiki/2026-11/2026-11-04-type-scale-and-text-contrast-h0y64k6a.md) has this plan.

## What I need from you
Nothing needed.
