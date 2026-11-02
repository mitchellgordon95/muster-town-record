---
id: "dc_ug4k44yfhn"
type: "note"
state: "building"
title: "Dead-code sweep 1: candidates and flags (kr_ef11f6ex28)"
authorId: "ag_ehvfty1gx3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["dead-code","sweep","flags","knip","kr_ef11f6ex28"]
createdAt: "2026-10-28T18:31:40.435Z"
updatedAt: "2026-10-28T20:03:24.426Z"
---
Sweep 1, findings only (no removals). main = live = 41236ee (GET /api/health commit, 2026-10-28 18:11Z). Assignment as_xp8fuautz6, from Mitchell's 1:1 [dc_fpui0p5b1y](../../meeting-notes/2026-10/2026-10-28-1-1-mitchell-and-mara-notes-ui0p5b1y.md) decision 2.

## Step 2 status (as_w48xxf79jl, 2026-10-28, pushed to main)
- Candidate 1 `sendError` (and its now-unused `FastifyReply` import): **removed in 0bb9a39**
- Candidate 2, the 4 dead locals/imports: **removed in 294031f**
- Candidate 3, `nanoid` in server and runtime: **removed in fb090bf**
- Candidate 6, the 5 auth barrel re-exports: **removed in ebbef6d**
- knip CI check: **added in 576fa3d**. It adds `knip.json`, `npm run check:deadcode` (`knip --include files,dependencies,unlisted,binaries`) and a CI `check` step after check:docs; root devDependencies now list knip, tsx, ws, @muster-town/core and @muster-town/schema; the unused tsx devDeps in cli, core and runtime are dropped. The README CI line mentions it (54b4d02).
- CI run 40759124041 (54b4d02, attempt 1): npm ci, check:docs, check:deadcode and typecheck pass. `npm test` fails on server manual.test.ts (docs/manual.md is 1924 words, cap 1900). That failure comes from 689761f (Pix), which went red before my commits (run 40758819469).
- `tsc --noUnusedLocals`: desk 0 and cli 0 findings. Core src 0 (only 4 in tests: lanes.test.ts:11 REPORT, verbs.test.ts:2 createBuilding and createResident, wakes-step5.test.ts:104 noor). Web not run (Workshop's code).
- Not touched: 4, 5, 7-14.

## Method and raw counts
- **knip@5** with a minimal knip.json (one entry per workspace: server src/main.ts, desk src/cli.ts, cli/core/runtime/schema src/index.ts, web src/main.tsx, root scripts/**). Raw: **5 unused files, 94 unused exports, 55 unused exported types, 3 unused deps, 3 unused devDeps, 4 unlisted deps, 2 unlisted binaries.**
- Hand triage of the 149 exports/types by grepping each name across packages/ and scripts/: **109 are used inside their own file** (only the `export` keyword is surplus), **39 share a name with another symbol elsewhere** (needs a typed check), **1 is used nowhere**.
- `tsc --noUnusedLocals`: see step 2 above.
- Route table: 133 server routes, each matched by regex against web/cli/desk/runtime/scripts/skills/manual. 10 had no client caller; 4 of those are by design (below).
- CSS: 403 classes in web/src/*.css; 21 have no literal reference, 14 of those are built dynamically, so **7 dead**.

## Candidates, ranked (safe first)
| # | What | Where | How verified unused | Risk | Status |
|---|---|---|---|---|---|
| 1 | `sendError` | server/src/context.ts:135 | knip; no other reference | none | removed in 0bb9a39 |
| 2 | `OPEN`, `TOWN_HALL_ID`, `canInteract`, `boardDocs` | core grants.ts, world.ts; server context.ts, routes/town.ts | tsc TS6133 | none | removed in 294031f |
| 3 | `nanoid` in server and runtime | package.json | knip + grep | none | removed in fb090bf |
| 4 | 7 dead CSS classes (`.doc-row-act`, `.funding-form`, `.resident-row`, `.review-box`, `.review-proposal`, `.review-title`, `.work-form`) | web/src/styles.css | no literal, not a dynamic prefix | low; Workshop's code | open |
| 5 | packages/legacy-web-alias | | its own "delete once live runs renamed code" | low; Workshop's | open |
| 6 | auth barrel re-exports (5) | server/src/auth/index.ts | knip | none | removed in ebbef6d |
| 7 | 109 surplus `export` keywords | rerun knip with exports | used only in their own file | none, low value | open (needed before knip checks exports) |
| 8 | BUDGET_POLICY dead branches | core lanes.ts, grants.ts, permissions.ts | the constant's value on main | Mitchell's switches | open |
| 9 | Rename P6 compat layer | ~20 files | docs/log.md "until P6" | medium: AGENT_TOWN_ADMINS may be a live Fly secret | open |
| 10 | REST grant drafting routes | server/src/routes/grants.ts | no client | documented public API | decide |
| 11 | Legacy single-VPS deploy files | deploy/ | README only | Prod's call | open |
| 12 | retire-placeholders script + route | scripts/, server | one-off | Bank: Mitchell | open |
| 13 | core/src/import-v0.ts | core/src/seed.ts | no collective uses `import` | low-medium | open |
| 14 | legacy/ | | nothing imports it | human decision | open |

Not dead (checked, keep): desk-slots admin API, POST /api/bank/drift, /auth/github/callback, /api/skills/:id/files/*, web mock/.

## Flags
Building columns (budgetMode, forks, codeAccess, explorationTokensPerDay, poolId), BUDGET_POLICY and desks.maxRunning are in Nell's inventory [dc_vie3wrhj54](../../../../bl_vef3v0oux0/docs/note/2026-10/2026-10-28-per-building-flags-where-each-is-set-who-flips-it-e3wrhj54.md). The code-level flags (BUDGET_POLICY.*, MUSTER_TOWN_DESKS.backend, desks.ghToken, MUSTER_TOWN_DEV, MUSTER_TOWN_DEPLOY_BRANCH, the AGENT_TOWN_* fallback, DESK_MODEL/DESK_MAX_TURNS, VITE_MOCK, VITE_USD_PER_MTOK, the backup secrets, FLY_DESKS_ACCESS_TOKEN) are unchanged from the sweep-1 table; see this doc's revision of 2026-10-28 18:31Z. All are live on prod or kept by design except the BUDGET_POLICY arms (candidate 8) and the AGENT_TOWN_* fallback (candidate 9).

## Next for knip
To add `exports` to check:deadcode: drop the 109 surplus `export` keywords and settle the 39 name-collision exports (~20k).

