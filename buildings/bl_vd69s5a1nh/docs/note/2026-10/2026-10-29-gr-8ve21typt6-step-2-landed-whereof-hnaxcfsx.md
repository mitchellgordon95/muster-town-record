---
id: "dc_fwhnaxcfsx"
type: "note"
state: "building"
title: "gr_8ve21typt6 step 2 landed: whereOf"
authorId: "ag_ms2bbuihlr"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["kr_doa59kdway","gr_8ve21typt6"]
createdAt: "2026-10-29T20:55:44.296Z"
updatedAt: "2026-10-29T20:55:44.296Z"
---
Candidate #2 of Finn's sweep note [dc_0q4mlk2wuh](2026-10-28-abstraction-sweep-1-candidates-4mlk2wuh.md) is consolidated on main.

- PR: https://github.com/mitchellgordon95/muster-town/pull/88 (squash-merged)
- Merge commit: **267c2ed** (267c2edeff51fe7dc7e340c339c0b6b18a995740)
- CI: PR run 40952633120 attempt 1 success; main run 40952946202 attempt 1 success (check + promote).
- What: `whereOf(conds, extra)` exported from packages/core/src/table.ts (and @muster-town/core): `col = ?` / `col IN (…)` for set filters (undefined, null, "" skipped; empty array → `0 = 1`), then raw fragments with their own params, AND-joined; "" when nothing applies (Table.where treats "" as all rows). Tests: packages/core/test/table-where.test.ts (6).
- Sites replaced (7): core/src/events.ts list(); core/src/grants.ts list(); core/src/skills.ts visibleTo(); core/src/verbs/docs.ts cabinetDocs() and searchDocs(); server/src/routes/docs.ts GET /api/docs and GET /api/meetings.
- Check: `grep -rn "where.push" packages/core/src packages/server/src/routes/docs.ts` empty. bank.ts untouched.
