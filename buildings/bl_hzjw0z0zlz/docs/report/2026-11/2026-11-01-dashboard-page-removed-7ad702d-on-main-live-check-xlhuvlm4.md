---
id: "dc_8oxlhuvlm4"
type: "report"
state: "building"
title: "Dashboard page removed (7ad702d on main); live check parked on its deploy"
authorId: "ag_4j04egrxuo"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["mt_ec2b7x80rg","dc_vzqoh7ppen"],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Approved: 7ad702d on main removes the Dashboard page, HUD ▤, KPI tiles and GET /api/kpis per Mitchell's 1:1 mt_ec2b7x80rg decision 1; join-funnel, objectives and the kpis table kept. The live check is already parked as as_mpzf99zfmb (resumes on deploy 7ad702d); as_uvkh7ghqru (\"user stats\" object, decision 2) was waiting on this assignment and can start. Rolls up once 7ad702d is live and checked."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-11-01T01:42:18.007Z"
sessionId: "se_x8p8zwlwga"
assignmentId: "as_bitdidbxsb"
costUsd: 1.0842451000000002
tokens: 54212
turns: 26
createdAt: "2026-11-01T01:42:07.591Z"
updatedAt: "2026-11-01T01:42:18.007Z"
---
## What I did
Removed the Dashboard page end to end per Mitchell's 1:1 mt_ec2b7x80rg (decision 1) and pushed **7ad702d** straight to main (seen on origin/main). Told Pix one line so the Workshop's sweep knows.

## Findings
- **Gone:** `packages/web/src/panels/DashboardPanel.tsx`; HUD ▤ button (hud.tsx); `"dashboard"` panel kind (state.ts, app.tsx); Town Hall "Dashboard / Open the dashboard" section (BuildingPanel.tsx); Goals tab's "(the town Dashboard shows them)"; meeting `dashboard` page ref (MeetingPanel.tsx, core meetings.ts PAGES, schema attach description); `api.kpis()` + `KpisView`; mock `kpis()`; `.kpi-*` and `.join-funnel` CSS; `GET /api/kpis` (server routes/grants.ts); `core/src/kpis.ts` (townKpis, kpiByKey (it had no users: grants.ts:177 reads `world.kpis` directly), KPI_WEEKS, JOIN_RETURN_DAYS); schema `KpiView`, `KPI_FRAMING`. Tests that exercised townKpis/api.kpis removed (core objectives "town KPIs" block, the Fund-KPI lines in member-funding, the web keyResults kpis lines).
- **Kept untouched:** `kpis` table and migration 043, `Kpi`/`KpiKey` schema (objectives still name a KPI), objectives routes and `set_objective` (whether objectives/KPI labels should go too is a separate question for Mitchell), `GET /api/join-funnel`, `POST /api/join-funnel/view`, the guest card ping. The mock fixture keeps the three KPI rows (without weekly values) because the mock objectives look up their name.
- **Docs:** goal-directed-budgets.md (status line notes the removal, API and UI lines struck), goals.md (UI inventory row → Removed), meetings.md (no `dashboard` attach). manual.md, README, skills had no Dashboard mention; manual at 1,874/1,900 words.
- **Checks:** `npm ci` (desk node_modules were stale), `npm run typecheck` green; core objectives/member-funding/meetings 24/24, web 213/213 (50 files), server access+hub 12/12; `check:docs` and `check:deadcode` (knip) clean.
- **Plan on resume (deploy 7ad702d):** curl /workshop/ for main-*.js and grep it for "The town goal as three KPIs" (expect none); `curl -o /dev/null -w %{http_code} https://muster.town/api/kpis` → 404; /api/join-funnel → 200; headless Chromium 1400×900 fresh profile (recipe [dc_bci4l87ab6](../../wiki/2026-10/2026-10-29-live-verification-on-muster-town-i4l87ab6.md)): HUD top bar shows $ and ? but no ▤, 0 console errors; one cropped picture of the HUD top bar.

## What I need from you
Nothing needed.
