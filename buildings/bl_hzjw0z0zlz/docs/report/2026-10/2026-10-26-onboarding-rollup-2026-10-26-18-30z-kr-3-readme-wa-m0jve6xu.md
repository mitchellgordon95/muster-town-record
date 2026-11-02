---
id: "dc_wam0jve6xu"
type: "report"
state: "building"
title: "Onboarding rollup 2026-10-26 18:30Z: KR 3 README walk done (second collective seeds in 3 min knowing the code, stalls from README alone); grant gr_ibccoje227 (8 M) awaits your decision; the push test needs your Docker Mac"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_stp4ibx4t5"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-26T18:16:55.143Z"
sessionId: "se_ej4zwatcko"
createdAt: "2026-10-26T18:14:48.125Z"
updatedAt: "2026-10-26T18:16:55.143Z"
---
## Shipped
Nothing new live since the 18:15Z rollup ([dc_ulahzs1fq5](2026-10-26-onboarding-rollup-2026-10-26-18-15z-pr-3-fresh-vis-ahzs1fq5.md)). Craig's PR 3 (eac2e24) redeploy is queued; his parked continuation live-checks it, then PR 4 (homepage pitch modal + square tiles, as_tzhxtwc9gh).

## Decided
- [dc_stp4ibx4t5](2026-10-26-kr-3-readme-walk-a-second-collective-seeds-in-3-mi-p4ibx4t5.md) (Kelly, KR 3 exploration, 2.02 M tokens) → **approve**. A fresh clone of eac2e24 seeds a second collective and answers /api/health in 3 min 05 s when you know the code (install 1 min 08 s, build 8 s, seed 3 s). From README.md alone it stalls: no start command for a collective other than the Workshop, scripts/serve.sh is zsh-only, no collective.json or registry example, README lines 3/5/23 still describe the retired climate collective. Code gap: home.ts:24-25 keys the registry match on url "/workshop/", so a second collective lists itself twice. Residents can't push code without Docker plus a Claude token in .env. 14 gaps with file:line fixes in [dc_5hz6sbfuhr](../../note/2026-10/2026-10-26-kr-3-readme-walk-2026-10-26-a-second-collective-st-z6sbfuhr.md).
- Filed grant proposal gr_ibccoje227 (8 M) for KR 3: one PR (README Run it as numbered steps with a quoted collective.json, start:collective script with serve.sh under bash, home.ts slug match, Docker hint on Code access, stale sentences gone), then a timed walk by a resident who has not read the code, plus one Docker-host push test.
- Edited kr_tzg9en02dh's how-to-check: there is no per-building repo, so it now reads "Code access on in Settings, naming the repo from collective.json; a resident's first session pushes a branch; Docker host with a Claude token". Keep or cut.
- Told Craig to key PR 4's tiles on the collective slug, not the url (no new assignment).

## Key results
- kr_z0mj5teeu7 (stranger path), gr_cm3zha6mk6 funded: 9,006,211 / 25,000,000 tokens; PRs 1-2 live, PR 3 pushed and awaiting redeploy, PR 4 queued.
- kr_1rpq0738sw (first minute): gr_vfyih8s6ri cut at checkpoint 18:05Z (4,546,164 / 4,000,000); on-track, no funded grant.
- kr_tzg9en02dh (README to second collective): not-started; gr_ibccoje227 proposed, 8 M ask, 0 spent. Exploration today 4,242,657 / 6,285,714.

## Needs from Mitchell
1. Fund, counter or reject gr_ibccoje227 in the Town Hall in-tray.
2. When its PR lands, run the push test on your Mac (Docker + CLAUDE_CODE_OAUTH_TOKEN in the new collective's .env): our desks have no Docker, so only you can confirm a resident pushes a branch on its first session.

## Key results I wrote (keep or cut: Building → Settings → Key results)
- edited kr_tzg9en02dh: "One person creates a new collective and its first coding building from the README alone in under 15 minutes, and its residents can push code on their first session." (how to check: Fresh clone on a Docker host with a Claude token, README.md with a stopwatch: the collective appears in the homepage list at /; its first building has Code access on in Settings, naming the repo from collective.json; a resident's first session pushes a branch. Under 15 min, no schema reads.; from [dc_stp4ibx4t5](2026-10-26-kr-3-readme-walk-a-second-collective-seeds-in-3-mi-p4ibx4t5.md), [dc_5hz6sbfuhr](../../note/2026-10/2026-10-26-kr-3-readme-walk-2026-10-26-a-second-collective-st-z6sbfuhr.md))
