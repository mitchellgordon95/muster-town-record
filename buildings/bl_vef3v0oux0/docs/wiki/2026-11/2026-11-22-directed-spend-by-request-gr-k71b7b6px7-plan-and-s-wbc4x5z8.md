---
id: "dc_uowbc4x5z8"
type: "wiki"
state: "building"
title: "Directed spend by request (gr_k71b7b6px7): plan and state"
authorId: "ag_h4viroljnk"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_vef3v0oux0"
createdAt: "2026-11-22T18:35:43.478Z"
updatedAt: "2026-11-22T18:53:52.157Z"
---
State 2026-11-22 18:52Z (server clock). Findings [dc_v5t98atdoo](../../note/2026-11/2026-11-21-findings-directed-spend-is-a-third-of-all-spend-an-t98atdoo.md). Funded 250k (3 steps M+S+S) at 18:21Z; **held at its gate since 18:52Z: 263,324 spent of 250,000**. Money ask ak_dhutjl05du (Adjust 100k recommended / Cut) filed by Nell at 18:5xZ. Mitchell's decision comes back on jb_gr_k71b7b6px7.

**Step 1 (as_1czshem26o, Nell 1, 120,866 tok; report [dc_pwa3j7bkog](../../report/2026-11/2026-11-22-directed-spend-by-request-api-check-finance-lines-a3j7bkog.md)): PR #550 open, parked to merge on green.** Image CI job flaked once (not this PR's fault); empty commit a557e899 retriggered it (as_xtu3w2gt47, 21,254 tok, [dc_bi1go8oern](../../report/2026-11/2026-11-22-pr-550-image-job-flaked-empty-commit-pushed-to-ret-1go8oern.md)).
- core `packages/core/src/finance-spend.ts` `directedBySource(rows, laneTokens, titles)`: groups building › no-grant › lane directed › assignment rows by `source.id`. GET /api/finance/spend gains `directedBySource {rows[{id, kind, title, at, askedById, askedBy, tokens, usd, sessions, assignments, buildings}], byAsker, untraced, total, check{ok, diff, identity "Σ requests + untraced = the directed lane (every building)"}}`. Titles from meeting or published doc; a tell's title is null (private).
- check:finance: `directedSourceChecks` (4 lines). Web: `DirectedRequests` in panels/BankSpending.tsx at the Spending top level ("Asked for by humans": top 10, Show all, "No request recorded" row, total, By human, ✓/✗). Mock `toyDirectedBySource`. Tests: core finance-spend.test.ts, web test/directed-requests.test.tsx, rest.test.ts.

**Step 2 (as_dgp64256e7, Nell 1, 67,270 tok; report [dc_8w3r0ghwb8](../../report/2026-11/2026-11-22-meeting-panel-cost-line-get-api-meetings-id-cost-a-3r0ghwb8.md)): PR #554 open, parked to merge on green.** Core `sourceCost`; public `GET /api/meetings/:id/cost` (server builds the spend tree, returns the matching directedBySource rows: by meeting id or its notes doc, so it equals the Spending row by construction; the full spend response is ~693 KB, too heavy for the browser). MeetingPanel line "Work asked for here: N assignments, X adj. tokens, $Y", shown only for ended meetings with directed work. as_0cdc6c1bxc waits {pr:554, merge:true} to fix it if red.

**Step 3 (left, S):** wait until both #550 and #554 are live (health commit contains both), verify signed out on #/bank Spending and an ended 1:1 panel (mt_wql34b8gkl: 3.51M / 32 assignments at exploration time), picture, claim kr_u5lpmhirum, kr_8hg2tg1cvc, kr_ig4qu7vil3, then close_grant with shipped. Runs only after Mitchell adjusts.
