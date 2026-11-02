---
id: "dc_ntaf4zvwul"
type: "report"
state: "building"
title: "Security advisories grant closed as done: PR #215 live (zod 4, @fastify/static 10, weekly audit gate), production deps clean of high/critical advisories"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_niizq5j8g6","dc_crwlir8gqm"],"urls":[]}
tags: ["rollup","grant-close"]
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-11-01T00:47:14.786Z"
sessionId: "se_34v6j8jv4g"
createdAt: "2026-10-31T22:23:32.720Z"
updatedAt: "2026-11-01T00:47:14.786Z"
---
Live: e487758 since 2026-10-31T22:21:37Z (/api/health).

## Shipped

**1. Production dependencies carry no high or critical security advisory, and a weekly audit gate keeps it that way**
**What it is:** PR #215 upgrades zod 3 → 4 and @fastify/static 8 → 10 in the server, runs `npm audit fix` for body-parser/fast-uri, and adds a GitHub Actions workflow `audit.yml` that runs `npm audit --omit=dev --audit-level=high` weekly and on every PR touching package*.json. The audit is its own workflow, not part of the deploy gate, so a red audit never blocks a redeploy. zod 4 broke 7 test files; all fixed in source. Grant gr_gh3lnuihw9 closed as done: 189,110 of 500,000 tokens spent, 310,890 returned to the Bank. Reports [dc_niizq5j8g6](2026-10-31-security-advisories-pr-215-merged-main-e487758-aud-izq5j8g6.md), [dc_crwlir8gqm](2026-10-31-security-advisories-grant-ready-to-close-e487758-i-wlir8gqm.md).
**What you'd see:** GitHub Actions, "audit" workflow on main: run 41247500734 green. Throwaway PR #218 (zod pinned back to 3.25.76): audit run 41247549368 red, naming GHSA-mrhx-c7xc-m3w5; closed unmerged. On a fresh main checkout `npm ci && npm audit --omit=dev --audit-level=high` exits 0 (only 3 glob/minimatch moderates with no upstream fix remain). https://muster.town/api/verbs returns 31 verbs, each with an inputSchema object and a description. API and CI only, no picture.
**Your call:** Mark the 5 key results of gr_gh3lnuihw9 met or missed from the Town Hall in-tray. Not done in the grant: vitest 4 (dev-only; npm 10.9.9 crashes installing it).

## Decided
- [dc_niizq5j8g6](2026-10-31-security-advisories-pr-215-merged-main-e487758-aud-izq5j8g6.md) (Mara 1, PR #215 merged → e487758, audit gate green on main and red on the zod-3 pin) → approve
- [dc_crwlir8gqm](2026-10-31-security-advisories-grant-ready-to-close-e487758-i-wlir8gqm.md) (Mara 1, e487758 live, /api/verbs lists an inputSchema for all 31 verbs) → approve; grant closed from this session

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_gh3lnuihw9 (closed, done) | kr_4jhab4c5cn no high/critical advisory goes unnoticed (audit workflow green on main) | claimed | 189,110 / 500,000 |
| gr_gh3lnuihw9 | kr_46398efa33 no high/critical advisory left in production deps | claimed | |
| gr_gh3lnuihw9 | kr_6805523069 the audit gate fails on a vulnerable dep (PR #218) | claimed | |
| gr_gh3lnuihw9 | kr_0800718a7a zod 4 changes nothing users see (/api/verbs, CI green attempt 1) | claimed | |
| gr_gh3lnuihw9 | kr_5a90181c60 the deploy gate is unchanged (ci.yml has no audit step) | claimed | |

No funded grant remains open in this building; the queue is empty. Today's spend by lane: exploration 150,281 tokens (free under the goal: 52,390), directed 198,566 tokens.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 0 proposals, 1 request ([dc_bn4s4m7cq3](../../../../../town-hall/outbox/2026-10/2026-10-29-redeploy-with-the-desk-image-rebuild-image-true-fo-4s4m7cq3.md)), 1 rollup ([dc_a995y60umi](2026-10-31-dead-exports-can-t-come-back-grant-gr-83jxsu8u0o-c-95y60umi.md))._
