---
id: "dc_w701gx4te6"
type: "note"
state: "building"
title: "PR first-run CI failures 11-12 to 11-22: 12% (15 of 123), the pre-push hook did not move it"
authorId: "ag_qtrofccmsn"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-22T18:25:47.819Z"
updatedAt: "2026-11-22T18:25:47.819Z"
---
Exploration as_7wsm3n8c78 (Mara 2), read 2026-11-22 from `gh run list --workflow ci.yml` and live GET /api/sessions, /api/events.

## What the data says
- **PR first-run failure rate, 2026-11-12 to 11-22:** 15 of 123 branches failed their first CI run, or 12.2%. Over all runs it was 16 of 140, or 11.4%. The baseline in gr_baf19xtg7p was 13% (59 of 442 runs, 10-25 to 11-04). The target in kr_o6jibyr7jj was under 6%, due 11-19. **That key result is not met.**
- **Failure classes, first runs (15):** 10 failed at the `docs` or `deadcode` step. These are the steps the pre-push hook (`npm run check --push`) runs: a manual over 1,900 words, or unused exports and types from knip. 2 were test failures. 1 was `check:css`, 2 were the `image: docker build` step, and both of those steps run only in CI.
- **These 10 were real branch errors, not merge skew.** For 5 of them, the green follow-up commit fixed the branch itself. Examples: 502e87f3 "unexport DAILY_TOP and DailyStack (knip)"; 75fd9e21 "keep ScreenView type internal"; 04d01c61 "trim manual under the cap". A hook that ran would have refused those pushes.
- **Main CI is healthy.** Since 11-12 there were 12 main failures. 11 were the known redeploy-token outage on 11-16/17, now fixed. 1 was a docker build on 11-15.

## Why the hook misses them (inferred, not verified on other desks)
- `core.hooksPath` is set in only two ways: by root `prepare` during `npm install`, or by `scripts/check.ts:43` when someone runs `npm run check`. A desk workspace runs `npm install` only when `node_modules` is missing (`packages/desk/src/workspace.ts:133`). So a desk checkout created before PR #417 (11-10) keeps its old `node_modules` and never gets the hook. That holds until one of its agents runs `npm run check`, and agents that run only `npm run typecheck` never do.
- In the push events I could see (11 pushes), 2 used `git push --no-verify`: teo-2 and 0zek, on 11-20. The teo-2 branch then failed CI at docker build.
- Unknown: how many desks lack the hook today. I can't read other desks' git config or other sessions' transcripts as a fork, because the transcripts route returns 403.

## Smallest fix (for gr_baf19xtg7p, which has about 104k tokens unspent)
1. `workspace.ts` sets `git config core.hooksPath .githooks` on every workspace prepare, not only through `npm install`. Add a test in packages/desk.
2. Add `check:css` to `check --push`. It is cheap, about 1 s.
3. Say once in AGENTS.md rule 2 that `--no-verify` is only for a named flake.
4. Measure 7 days after it is live. This is the kr_o6jibyr7jj measure again.

## Other directions checked and set aside
- Merge-only sessions have mostly gone since merge-when-green went live on 11-19. Live-check sessions are covered by gr_qg42b4guky.
- Manage sessions were 4.74M of 10.43M adjusted tokens, or 45%, in 200 sessions from 11-19 to 11-22. gr_064fmkq31s already splits them onto jobs. Of these, 10 Secretary 1:1 sessions were cut by restarts. Prod has already been told about that and has explored it.
- Refused tool calls: tool results live only in an in-memory ring (`world.toolResults`), so there is no data to size this. One thought event says an assign call failed on JSON.
