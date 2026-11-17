---
id: "dc_dv10aswei3"
type: "report"
state: "building"
title: "Forecast asks stopped in PR #496; parked on its CI"
authorId: "ag_22abqnnbf8"
authorKind: "agent"
buildingId: "bl_vd69s5a1nh"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Parked on PR #496 CI; as_kzhk2giibq (waiting {pr:496}) merges it when green. Nothing to add. The live dictionary line on \"gate\" (dc_rcl65iznnx) goes to the Secretary."
decidedBy: "ag_croreod6q3"
decidedAt: "2026-11-17T18:43:40.412Z"
sessionId: "se_klfr5g5kz7"
assignmentId: "as_z0a886fw3j"
costUsd: 1.514982
tokens: 75749
turns: 27
createdAt: "2026-11-17T18:43:30.684Z"
updatedAt: "2026-11-17T18:43:40.412Z"
---
## What I did
Took out the forecast gate per Mitchell's decision 2 in mt_vdu3iqhasi. Added a boot repair, updated the docs and tests, and opened draft PR #496 (https://github.com/mitchellgordon95/muster-town/pull/496, head 986ee9f0). I am parked until its CI finishes.

## Findings
- **Code.** `fileForecast` no longer files a need when a forecast goes over the ceiling. What it still records: `forecast` and `needsTopUp` on the grant, plus the `grant.forecast` and `grant.top-up-needed` events. A forecast within the ceiling still files a `gate` notice. I removed `needAtForecast`. `gateFacts` now only describes the held case (its `held` flag and the "projected past" note are gone), and `needAtCheckpoint` lost its `forecast` argument. `templateCardsToNeeds` now writes a gate need only for a grant in checkpoint. The 100% hold in `Grants.checkpoints` is the only gate, with no tolerance.
- **retireGateAsk dropped.** Its only job was to retire a forecast-filed gate ask on a funded grant when a later forecast came back within the ceiling. It skipped any grant not in funded status, so it never touched a held grant's ask. Since no forecast files such an ask any more, it had nothing left to do.
- **Live check: a repair was worth writing.** One forecast gate ask is open now: ak_8ucpj7lump, "Adjust the day-by-day chart grant by 50,000 tokens", on gr_epbcgb0hvs (funded, 200,000 ceiling, needsTopUp true). The new boot repair `retireForecastGates` (world.ts, runs right after `backfillAsks`) handles it. On every funded grant it retires each live Adjust/Cut ask and settles each open gate need, with a note citing mt_vdu3iqhasi decision 2. It leaves held grants alone, can run more than once safely, and is tested.
- **Docs.** Updated docs/invariants/grants.md (invariant 12 rewritten with 6 test citations, and the edge in invariant 1), docs/legible-delegation.md (§7.3 point 4 marked as changed on 2026-11-17, plus build step 7, the file map and needs line), docs/manual.md (one line) and the JSDoc in grant-forecast.ts and notices.ts. I also changed the dictionary seed for "gate". That seed is only used when the dictionary is first created, so the live dictionary doc [dc_rcl65iznnx](../../../../town-hall/docs/dictionary/2026-11/2026-11-09-town-dictionary-l65iznnx.md) still says a forecast past the ceiling is a gate. Whoever owns that doc (the Secretary, I expect) needs to change that line. Added docs/log.d/2026-11-17-stop-the-forecast-asks.md.
- **Tests.** forecast-asks.test.ts now checks that a forecast over the ceiling files no need and no ask while the forecast and its events are still recorded. It also tests the held gate's need and facts, adjusting at the hold, and the boot repair. The whole core suite passes (1081 of 1081), and `npm run check --fast` passes (7m11s).
- **Should be live:** 986ee9f0, once it is merged and CI deploys main.

## What I need from you
Nothing needed. I merge #496 myself when CI is green.
