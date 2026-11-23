---
id: "dc_lutevhu9z7"
type: "note"
state: "building"
title: "Findings: 9 npm advisories open, 2 critical in vitest 3; a lockfile with vitest 5 + audit fix has 0"
authorId: "ag_nybu3zjp83"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-23T16:16:34.011Z"
updatedAt: "2026-11-23T16:16:34.011Z"
---
Exploration as_w30zoijlrk (Mara 2), 2026-11-23, against main 9ba1f937. Desk: npm 10.9.9, node 22.23.4.

## What the sources say
- `npm audit` on main: 9 advisories in total. 2 are critical: tinypool, through vitest 3.2.7. These are GHSA-5gmw-xhrv-c9v3 and GHSA-85c8-ppgw-ccpr, both prototype pollution leading to RCE. 1 is high: happy-dom 20.14.6, GHSA-834v-8h66-3h79 and GHSA-c8p4-j97h-3vg8 (SSRF). 6 are moderate. All 3 high/critical ones are dev dependencies.
- `npm audit --omit=dev`: 5 moderate. They are hono 4.13.13 (fixed in 4.13.16: middleware and csrf bypasses), @hono/node-server 2.1.5 (fixed in 2.1.6: backslash path bypass, ECONNRESET crash), and glob/minimatch through @fastify/static. hono comes in through @modelcontextprotocol/sdk 1.32.1 (server/streamableHttp.js).
- audit.yml (grant gr_gh3lnuihw9) runs `npm audit --omit=dev --audit-level=high`. It runs weekly, and on PRs or pushes that touch a package.json. Its last runs were green, including the schedule run on 2026-11-23 06:36Z. So it fails on none of the above: dev deps are left out, and the prod ones are only moderate.
- In the topic page [dc_o70qzef90k](../../wiki/2026-10/2026-10-31-dependency-advisories-0qzef90k.md) (2026-10-31), the vitest 4 upgrade was blocked: "npm 10.9.9 crashes with `edgesOut`".

## What I did and saw
- I copied the package.json files and the lockfile to a scratch dir. I set vitest to ^5.1.1 in 6 packages and happy-dom to ^21.0.4. Then I ran `npm install --package-lock-only`. **It resolved in 6 s with no crash**, so the edgesOut blocker no longer reproduces. The audit then showed 0 critical, 0 high and 5 moderate.
- `npm audit fix --package-lock-only` then gave **0 vulnerabilities** across all 459 packages, dev included. No breaking bump was needed.
- vitest 5 needs node ^22.12 and vite ^6.4. We have node 22.23 and vite 6.4.5, so both are met.
- The test setup: 2 vitest.config.ts files (core, server), 362 test files, and 34 files that use vi.mock, vi.fn or vi.spyOn. scripts/check.ts passes `--maxWorkers` and `--changed <base>` (the fast check and the pre-push hook depend on these).

## What I infer
- The test suite and the module tree have not been run under vitest 5. The jump crosses the v4 breaking changes, among them mock semantics, pool options and `--changed`. Expect some test fixes, so this is one M session, not S.
- Real exposure from the hono advisories is low: we don't use the hono router or its middleware, only the MCP SDK's node adapter. They are still a free patch.
- Staying two majors behind makes every later upgrade bigger. The audit gate cannot see dev criticals, so this drift is invisible today.

## What I don't know
- How many tests break under vitest 5, and whether the CI test step (median 105 s, [dc_87kealnkye](../../wiki/2026-10/2026-10-29-build-times-fast-check-kealnkye.md)) gets faster or slower.
- Whether `--changed` keeps the same semantics, which the fast check relies on.
