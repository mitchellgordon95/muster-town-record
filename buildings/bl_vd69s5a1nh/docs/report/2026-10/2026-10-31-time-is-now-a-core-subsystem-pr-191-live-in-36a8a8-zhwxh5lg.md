---
id: "dc_n0zhwxh5lg"
type: "report"
state: "building"
title: "Time is now a core subsystem (PR #191 live in 36a8a86): every brief opens with the server clock and guessed stamps get a warning; new KR kr_4jhab4c5cn (3 high advisories in production deps); both funded grants' first steps are running on forks"
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_op3e6s9iov","dc_voahxk4og1"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-31T21:11:08.265Z"
sessionId: "se_br7he1wzdk"
createdAt: "2026-10-31T21:03:15.779Z"
updatedAt: "2026-10-31T21:11:08.265Z"
---
Live: 36a8a86 (contains b72c9dc, PR #191).

## Shipped

**1. Time in words: one place a time becomes text, and the clock in every brief**
**What it is:** Your ask in Pix's 1:1 (time usage owned by this building). A new core module formats a time for an agent as a server-read stamp and for a human as a duration from now; all 15 hand-sliced "HH:MM UTC" sites in core now use it. Work briefs, 1:1s and meeting replies open with "Clock: it is <server stamp> as this starts" plus the rule to write only server-read times. A hand-written "~20:50Z" or "about 21:25 UTC" in a wiki page, log, report or meeting line is filed but comes back with a warning naming it. PR #191 → b72c9dc; report [dc_voahxk4og1](2026-10-31-time-usage-is-now-a-core-subsystem-pr-191-b72c9dc-ahxk4og1.md); page "Time in words" [dc_l7og22m4zq](../../wiki/2026-10/2026-10-31-time-in-words-og22m4zq.md).
**What you'd see:** Start any 1:1: the agent's first line carries the server clock and transcript lines carry their stamp. No picture: prompt and API text only. Left out on purpose: durations in the web UI (Workshop's or UI/UX's call) and the team-lead brief, which still has no clock line; a queued check (as_2kz7aqlu6g) verifies the live behaviour and tells Pix.
**Your call:** Whether you want "20 min ago" durations on screen in the web UI too (then it is a Workshop or UI/UX ask).

**2. New key result: no high or critical advisory in production dependencies goes unnoticed**
**What it is:** Mara 1's exploration found 3 high advisories in production deps (zod 3.25, @fastify/static 8.3, body-parser 2.3), two published this month, with Dependabot off and no audit in CI. Exposure is modest today (static plugin serves only the web build, bodies capped at 1 MB). New KR kr_4jhab4c5cn; you funded the plan at 500,000 tokens (asked 110,000). Findings [dc_zytvyrq15d](../../note/2026-10/2026-10-31-findings-known-vulnerable-production-dependencies-tvyrq15d.md), report [dc_op3e6s9iov](2026-10-31-production-deps-carry-3-high-security-advisories-a-3e6s9iov.md).
**What you'd see:** Nothing yet. When the PR lands: a green "audit" workflow on main, `npm audit --omit=dev --audit-level=high` exits 0, and /api/verbs still lists every verb's schema after the zod 4 move. API-only; no picture.
**Your call:** None (the KR is listed below for you to keep or cut).

## Decided
- [dc_voahxk4og1](2026-10-31-time-usage-is-now-a-core-subsystem-pr-191-b72c9dc-ahxk4og1.md) → approve (PR #191 live; its parked continuation cancelled, replaced by the small directed verification as_2kz7aqlu6g so there is one rollup, not two).
- [dc_op3e6s9iov](2026-10-31-production-deps-carry-3-high-security-advisories-a-3e6s9iov.md) → approve (KR written, grant funded by you at 500k).
- The two "grant funded: assign its first step" notices were done here and cancelled: gr_83jxsu8u0o step 1 (the whole knip PR) is as_ftg6pn24f1, gr_gh3lnuihw9 step 1 (the whole zod 4 + audit.yml PR) is as_cvgu0h7kp0, both on forks in parallel. Each is one PR, merged on green and redeployed; the security one stops early with a report if zod 4 breaks more than about 20 test files.

## Key results
| Key result | Status | Grant | Spent / granted |
|---|---|---|---|
| kr_ealc55cjf5 Dead exports can't come back (knip exports+types in check:deadcode, 207 → 0) | not-started, step 1 queued | gr_83jxsu8u0o | 0 / 200,000 |
| kr_4jhab4c5cn No high/critical advisory in production deps goes unnoticed (new this session) | not-started, step 1 queued | gr_gh3lnuihw9 | 0 / 500,000 |

Today's spend by lane: exploration 150,281 tokens (free under the goal: 726,221), directed 177,581 tokens (PR #191 was the bulk: 161,235).

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 0 proposals, 1 request ([dc_bn4s4m7cq3](../../../../../town-hall/outbox/2026-10/2026-10-29-redeploy-with-the-desk-image-rebuild-image-true-fo-4s4m7cq3.md)), 0 rollups._

## Key results I wrote (keep or cut: Building → Settings → Key results)
- created kr_4jhab4c5cn: "No known high or critical security advisory in production dependencies goes unnoticed: `npm audit --omit=dev --audit-level=high` is clean on main and a dependency-audit workflow runs it weekly and on every PR that changes package.json or package-lock.json (from 3 high at 36a8a86)." (how to check: GitHub Actions: the "audit" workflow's latest run on main is green; `npm audit --omit=dev --audit-level=high` on a fresh main checkout exits 0; a PR that pins zod back to 3.25 makes the audit workflow fail naming zod.; from [dc_zytvyrq15d](../../note/2026-10/2026-10-31-findings-known-vulnerable-production-dependencies-tvyrq15d.md))
