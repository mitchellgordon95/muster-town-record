---
id: "dc_op3e6s9iov"
type: "report"
state: "building"
title: "Production deps carry 3 high security advisories and nothing checks for them: new KR kr_4jhab4c5cn, proposed gr_gh3lnuihw9 (110k)"
authorId: "ag_euey35vx78"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_zytvyrq15d","dc_o70qzef90k"],"urls":["https://github.com/advisories/GHSA-mrhx-c7xc-m3w5","https://github.com/advisories/GHSA-83w8-p2f5-377r","https://github.com/advisories/GHSA-27r3-jxmh-p828"]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Approved. Mitchell funded gr_gh3lnuihw9 at 500k (asked 110k); its first step goes on the building queue from this team-lead session."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-10-31T21:01:38.715Z"
sessionId: "se_h1xtgj64zb"
assignmentId: "as_ho9igbbgto"
costUsd: 1.2109224000000003
tokens: 60546
turns: 32
createdAt: "2026-10-31T20:57:48.764Z"
updatedAt: "2026-10-31T21:01:38.716Z"
---
## What I did
Checked three directions on main 36a8a86: duplicated code, type-safety escapes and dependency advisories. Duplication is only 0.45% by jscpd, and its biggest clone is desk/sdk.ts, already held because it's token code. There are 13 `any` or ts-ignore escapes. Dependency advisories were the real gap, so I went deep on them. I used a scratch copy on my desk to work out what fixing them would take. Nothing was pushed. I wrote findings [dc_zytvyrq15d](../../note/2026-10/2026-10-31-findings-known-vulnerable-production-dependencies-tvyrq15d.md) and topic page "Dependency advisories" [dc_o70qzef90k](../../wiki/2026-10/2026-10-31-dependency-advisories-0qzef90k.md), set KR kr_4jhab4c5cn and proposed gr_gh3lnuihw9.

## Findings
- **Production dependencies:** `npm audit --omit=dev` finds 3 high and 3 moderate advisories.
  - **zod:** the server, schema and web packages use zod 3.25.76. It is affected by GHSA-mrhx-c7xc-m3w5, published 10-01 (memory exhaustion).
  - **@fastify/static 8.3.0:** four advisories, including GHSA-83w8-p2f5-377r (high, route-guard bypass).
  - **body-parser 2.3.0:** pulled in by the MCP SDK; GHSA-27r3-jxmh-p828, published 10-23 (DoS).
- **Dev dependencies:** 2 critical, in tinypool under vitest 3.2.7.
- **Nothing notices new advisories:** Dependabot alerts are disabled on the repo (the API returns 403), and CI never runs an audit.
- **Exposure today is modest:** the static plugin only serves the public web build, and fastify caps request bodies at 1 MB. But two of the three highs were published this month and nobody would have seen them.
- **A trial fix works:** zod ^4.6.7, @fastify/static ^10.1.8 and `npm audit fix` leave **0 high or critical** in production deps. Three moderates remain (glob/minimatch), with no upstream fix yet. The typecheck then shows 37 errors, and 23 of them are in one hand-written zod-3 JSON-schema converter, which zod 4's built-in `z.toJSONSchema` can replace.
- **The audit can't go in the deploy gate.** ci.yml promotes a green main to prod, so a newly published advisory would freeze deploys, and `npm audit` depends on the registry being up. The plan puts it in its own workflow that runs weekly and on PRs that change package*.json.
- **vitest 4 is a stretch goal:** it fixes the dev criticals, but npm 10.9.9 crashes trying to install it here.
- **Proposal gr_gh3lnuihw9 (110k):** one PR, merge and redeploy. It stops early with a report if the zod 4 migration breaks more than about 20 test files. It has no git hook, so it doesn't repeat the plan rejected three times on PR #71.

## What I need from you
Nothing needed.
