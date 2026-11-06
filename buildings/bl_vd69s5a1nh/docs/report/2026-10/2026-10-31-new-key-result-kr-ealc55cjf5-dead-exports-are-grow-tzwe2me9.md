---
id: "dc_9ytzwe2me9"
type: "report"
state: "building"
title: "New key result kr_ealc55cjf5: dead exports are growing again (149 → 207 in 3 days); proposal gr_83jxsu8u0o is in your in-tray. Nothing shipped."
authorId: "ag_croreod6q3"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":["dc_ipcpcdwqog"],"urls":[]}
tags: ["rollup"]
verdict: "stop"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-31T20:37:56.069Z"
sessionId: "se_15tyhe4qjz"
createdAt: "2026-10-31T20:27:07.482Z"
updatedAt: "2026-10-31T20:37:56.069Z"
---
Live: e41f375 (Pix's #181 and Nell's #180; nothing from this building since 34b7e53).

## Shipped
Nothing shipped from this building since the last rollup ([dc_jela5ondmt](2026-10-31-gr-vipnoft4gk-closed-as-done-the-manual-s-word-cap-la5ondmt.md)). This rollup exists because a key result was written.

## Decided
- [dc_ipcpcdwqog](2026-10-31-dead-exports-are-growing-again-149-207-in-3-days-d-cpcdwqog.md) → approve. Mara 1 ran knip with exports and types at 9fe1873: 141 unused exports plus 66 unused types (207), up from 149 on 10-28. Two are dead functions (web `Feed` in panels/ui.tsx, `placeAt` in state.ts); 118 only need the `export` keyword removed. Adding the checks costs about 0.3 s. Findings in [dc_qortjdoqsd](../../note/2026-10/2026-10-31-dead-exports-are-back-knip-s-deferred-exports-chec-rtjdoqsd.md).

## Key results
| Key result | Status | Spent / granted |
|---|---|---|
| kr_ealc55cjf5 Dead exports can't come back (knip exports+types in check:deadcode, 0 unused) | not-started, no funded grant | 0 / 0 (proposal 70k open) |
| kr_939kp3vjxc Fast check | claimed, awaiting your mark | gr_75eq6h3ltp closed |
| kr_8wilbokqcn Observable timings | edited 10-30, weekly watch fires 2026-11-06 | no grant |

Today's spend by lane: exploration 89,735 tokens (free under the goal: 4,344,603), directed 16,346 tokens.

## Needs from Mitchell
Nothing needed. The grant proposal for the new key result is already in your in-tray; its note says the `export`-keyword removals touch other buildings' files, so funding it is also the permission to do that.

_Already waiting in your in-tray: 1 proposal (gr_83jxsu8u0o), 1 request (dc_bn4s4m7cq3), 1 rollup ([dc_jela5ondmt](2026-10-31-gr-vipnoft4gk-closed-as-done-the-manual-s-word-cap-la5ondmt.md))._

## Key results I wrote (keep or cut: Building → Settings → Key results)
- created kr_ealc55cjf5: "Dead exports can't come back: `npm run check:deadcode` (CI) includes knip's exports and types checks and is green on main, with 0 unused exports/types (from 141 + 66 at 9fe1873)" (how to check: package.json check:deadcode includes exports,types; the CI check job on main is green; a PR adding an unused exported function fails check:deadcode naming it.; from [dc_qortjdoqsd](../../note/2026-10/2026-10-31-dead-exports-are-back-knip-s-deferred-exports-chec-rtjdoqsd.md), [dc_vwlbhi4lx0](2026-10-28-dead-code-sweep-1-14-candidates-and-a-code-level-f-lbhi4lx0.md))
