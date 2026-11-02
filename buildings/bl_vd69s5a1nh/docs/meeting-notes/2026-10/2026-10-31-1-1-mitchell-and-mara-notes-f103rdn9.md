---
id: "dc_3jf103rdn9"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Mara — notes"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-31T20:03:47.014Z"
updatedAt: "2026-10-31T20:03:47.014Z"
---
# 1:1: Mitchell and Mara

Kind: one-on-one. Facilitator: Mara. Attendees: Mara. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Mitchell:** I'd like to talk about your report "Nothing shipped since 03beade; CI exploration found no flakes and one recurring toil (the manual's word cap). Your call…" ([dc_akibptfvlo](../../report/2026-10/2026-10-31-nothing-shipped-since-03beade-ci-exploration-found-ibptfvlo.md)). (presented: [Nothing shipped since 03beade; CI exploration found no flakes and one recurring toil (the manual's word cap). Your call: keep the kr_8wilbokqcn edit and mark it met](../../report/2026-10/2026-10-31-nothing-shipped-since-03beade-ci-exploration-found-ibptfvlo.md))
- **Mara:** Hi Mitchell. The short version of that rollup: nothing shipped from this building since 03beade, and two explorations found main is healthy (no flakes or re-runs in 200 runs; check total median 94 s, no slowdown). The one recurring toil is the manual's 1900-word cap: 10 commits since 10-28 only trimmed docs/manual.md, and main sits at 1890/1900. The fix is the 30k proposal gr_vipnoft4gk (fail fast in check:docs, no pre-push hook); the 60k one gr_9nvxjgajh6 is the earlier draft and should be rejected. The one thing I asked you for is to keep the kr_8wilbokqcn edit and mark it met. What did you want to go over?
- **Mitchell:** what is the key result? and what does your prop do
- **Mara:** The key result is kr_cm5qb2wqh7: "CI on main stays green without reruns: flaky tests get fixed at the root, not retried." Check: the last 20 main runs on GitHub Actions pass on the first attempt. It's on-track today; the exploration found no flakes.

What the proposal (gr_vipnoft4gk, 30k) does: today the manual's 1900-word cap is a Vitest test in packages/web/test/manual.test.ts, so a feature that adds a paragraph to docs/manual.md only fails at the tests step, about 90 s in, and then needs a separate trim commit. Ten such trim commits since 10-28. The proposal moves the cap into the docs step (check:docs), which runs in under a second and prints the word count and overage, so the author sees it on the first local run and fixes it in the same commit. It deletes the Vitest cap test, keeps the 1900 number, one PR. It does not add a pre-push hook; that was the part of the 60k draft you rejected before.

## Decisions

(none)
