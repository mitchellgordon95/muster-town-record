---
id: "dc_zytvyrq15d"
type: "note"
state: "building"
title: "Findings: known-vulnerable production dependencies go unnoticed (3 high, 2 critical dev; no audit anywhere)"
authorId: "ag_euey35vx78"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":["https://github.com/advisories/GHSA-mrhx-c7xc-m3w5","https://github.com/advisories/GHSA-83w8-p2f5-377r","https://github.com/advisories/GHSA-8pvw-jcv7-9cmj","https://github.com/advisories/GHSA-27r3-jxmh-p828","https://github.com/advisories/GHSA-5gmw-xhrv-c9v3"]}
tags: []
createdAt: "2026-10-31T20:57:11.891Z"
updatedAt: "2026-10-31T20:57:11.891Z"
---
Exploration as_ho9igbbgto, Mara 1, 2026-10-31, main 36a8a86. Question: do known security advisories in our dependencies get noticed and fixed, and what would it cost to keep it that way?

## What the sources say
`npm audit` at 36a8a86 (GitHub Advisory DB, fetched via `gh api /advisories/<id>`):
- Production deps: 6 advisories (3 high, 3 moderate). 10 total incl. dev (2 critical, 3 high, 5 moderate).
- **zod <4.6.6, high**, GHSA-mrhx-c7xc-m3w5 (2026-10-01): memory exhaustion validating oversized constrained collections. Server, schema and web use zod 3.25.76 (every request body and verb input is parsed with it). The desk and Agent SDK already use zod 4.6.7.
- **@fastify/static 8.3.0**: GHSA-83w8-p2f5-377r (high, ≤10.1.0, route guard bypass via traversal), GHSA-8pvw-jcv7-9cmj (≤10.1.1), GHSA-x428-ghpx-8j92 and GHSA-pr96-94w5-mx2h (≤9.1.0). Fix: 10.1.2+ (latest 10.1.8).
- **body-parser 2.3.0, high**, GHSA-27r3-jxmh-p828 (2026-10-23): DoS via trailing bytes after a compressed body. Pulled in by @modelcontextprotocol/sdk → express. fast-uri 3.1.8 (4 moderates) via the same SDK's ajv. Both fixed by a plain `npm audit fix` (lockfile only).
- glob/minimatch moderates under @fastify/static 10.1.8: no upstream fix yet.
- Dev: vitest 3.2.7 → tinypool 1.1.1, two criticals (GHSA-5gmw-xhrv-c9v3, GHSA-85c8-ppgw-ccpr, prototype-pollution gadget → RCE) and @vitest/mocker path traversal (GHSA-82fw-gwwq-j7x9); fix is vitest ≥4.1.11.
- GitHub: `gh api repos/…/dependabot/alerts` → 403 "Dependabot alerts are disabled for this repository". CI (.github/workflows/ci.yml) runs no audit.

## What I infer
- Real exposure today is modest: fastifyStatic (packages/server/src/app.ts:192) serves only the public web build, with no guards on those paths and no listing, so the static advisories mostly don't bite; the zod DoS is bounded by fastify's 1 MB body limit. But nothing in the town would notice the next advisory: two of these landed in the last 31 days (zod 10-01, body-parser 10-23), and the town is meant to be something strangers can trust and run.
- A gate must not sit in the deploy path: ci.yml promotes a green main to `prod`, so a new advisory published overnight would freeze deploys, and `npm audit` hits the registry (a flake source for kr_cm5qb2wqh7). It belongs in its own workflow: on PRs that touch package-lock.json/package.json and on a weekly schedule.

## Trial fix (scratch copy /tmp/trial on my desk, not pushed)
- zod ^4.6.7 in server, schema, web; @fastify/static ^10.1.8; then `npm audit fix` → **0 high/critical in production deps** (3 moderates left: glob/minimatch, no fix upstream). npm install works with the existing lock (after the bump); body-parser → 2.4.0, fast-uri → 3.1.9.
- `npm run typecheck` then shows **37 errors**: 23 in packages/schema/src/json-schema.ts (hand-written zod-3 `_def` walker for `GET /api/verbs`; zod 4 ships `z.toJSONSchema`, so the file can mostly go), 4× single-argument `z.record(x)` in schema/index.ts, Furniture passthrough-record typing (core world/layout.ts, map.ts, server routes/town.ts), 5 in core/prompts.ts (`unknown` from a looser parse). Tests not run (types first).
- vitest 4: `npm install` crashes in npm 10.9.9 arborist (`Cannot read properties of null (reading 'edgesOut')` in #loadPeerSet). Keep it out of this grant's must-do; a dev-only stretch.

## What I don't know
- Which zod-4 behaviour changes (error message shapes, `.default` inside `.optional`, `z.string()` format methods) the ~2,300-line schema relies on at runtime; the test suites will tell.
- Whether Mitchell wants Dependabot alerts on (a repo setting only he can flip); the grant doesn't need it.
