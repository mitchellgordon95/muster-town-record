---
id: "dc_77jyudloy8"
type: "report"
state: "building"
title: "Workshop rollup 19: objectives and KPIs live (6c80fe4), the Workshop's three objectives entered, two new key results with a proposal each (gr_f5bmciloqy, gr_tvt32g9xly) for you to decide; Bank grant at 98%"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_wd61y6ekd9","dc_y93vhb84ec","dc_30ydg6hj3c","dc_s8x64wdxsv","dc_k80u3dnsgr","dc_0dtuod5bsd"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decisionNote: "Superseded by a decision in meeting \"Town Hall town-hall\": Workshop: FLY_DESKS_ACCESS_TOKEN is now granted town-wide. Pix assigns Root the image:true redeploy and the check that desk sessions post real token counters. T"
decidedBy: "ag_mh0qidzgw6"
decidedAt: "2026-10-27T17:42:52.857Z"
sessionId: "se_e1jne2drcc"
createdAt: "2026-10-27T07:06:17.435Z"
updatedAt: "2026-10-27T17:42:52.857Z"
---
## Shipped
- **Objectives and KPIs live** (Lena, 6c80fe4, [dc_30ydg6hj3c](2026-10-27-objectives-and-kpis-built-and-pushed-to-main-6c80f-ydg6hj3c.md), live check [dc_wd61y6ekd9](2026-10-27-6c80fe4-live-api-kpis-returns-fund-join-and-trust-61y6ekd9.md)): each building goal holds up to 3 objectives, each naming the KPI it moves (Fund, Join, Trust) and holding up to 4 key results. GET /api/kpis returns the three KPIs over 8 weekly windows; the Dashboard (HUD ▤) opens for guests with KPI tiles and every building's objectives. All three KPIs read 0 this week and last: correct, because every funding and join event so far is yours and the owner is excluded.
- **Several grant proposals per building live** (Root, ee536a5 in 6c80fe4, [dc_s8x64wdxsv](2026-10-27-red-ci-on-ee536a5-is-fixed-main-is-green-at-6c80fe-x64wdxsv.md), [dc_k80u3dnsgr](2026-10-27-ee536a5-is-live-and-the-board-returns-proposals-no-0u3dnsgr.md)): the board returns proposals[], the Town Hall in-tray lists each open proposal on its own row, each decided on its own. Seen live with the Workshop's two proposals ([dc_y93vhb84ec](2026-10-27-workshop-objectives-entered-live-trust-join-fund-o-3vhb84ec.md)).
- **Wake step 4 live** (Keel, 49aeb33, [dc_0dtuod5bsd](2026-10-27-wake-step-4-49aeb33-is-live-ci-green-prod-and-api-tuod5bsd.md)): the Waker runs over the event log with a persisted cursor; the post-boot wake fired through it.
- **Workshop objectives entered** (me, [dc_y93vhb84ec](2026-10-27-workshop-objectives-entered-live-trust-join-fund-o-3vhb84ec.md)), 2026-Q4, from Lena's design and our 1:1 mt_akz25kqo2q: ob_s7jsvvoe5p Trust "a funder can see exactly what every token bought" (kr_vyrhhiyotb under it); ob_508f35a2m4 Join "a stranger finishes useful work in their first session"; ob_qieolu8bvs Fund "someone other than Mitchell funds a key result end to end".

## Decided
- [dc_wd61y6ekd9](2026-10-27-6c80fe4-live-api-kpis-returns-fund-join-and-trust-61y6ekd9.md) (Lena, 6c80fe4 live check): approved. Her one open item, the grouped views with real objectives, is now Lena's as_syvtmi9dkd (read-only live check of board, desk brief, Settings, Dashboard).
- [dc_y93vhb84ec](2026-10-27-workshop-objectives-entered-live-trust-join-fund-o-3vhb84ec.md) (me, objectives entered): approved, folded here.
- [dc_30ydg6hj3c](2026-10-27-objectives-and-kpis-built-and-pushed-to-main-6c80f-ydg6hj3c.md), [dc_s8x64wdxsv](2026-10-27-red-ci-on-ee536a5-is-fixed-main-is-green-at-6c80fe-x64wdxsv.md), [dc_k80u3dnsgr](2026-10-27-ee536a5-is-live-and-the-board-returns-proposals-no-0u3dnsgr.md), [dc_0dtuod5bsd](2026-10-27-wake-step-4-49aeb33-is-live-ci-green-prod-and-api-tuod5bsd.md): approved earlier today (build, red-CI fix, live checks). The red main ee536a5 was a real web typecheck error, fixed in 6c80fe4; residents now typecheck all packages including web before pushing.
- Root's parallel-proposals live check as_hiqqe287fg is running; nothing else queued.

## Key results
- kr_vyrhhiyotb (Trust, on-track), grant gr_iq5m7dug56: 1,640,037 / 1,666,667 tokens (98%). The checkpoint comes at 100%; step 4 (calibration against real cost) is what remains.
- Key results I wrote today (keep or cut):
  - kr_4li00ad46e under Join (not-started): a connected visitor agent's first look carries a starter brief plus one offered task, and its first-session report reaches a human in-tray. Proposal gr_f5bmciloqy, 250,000 adjusted tokens.
  - kr_6f9c200vsx under Fund (not-started): a member with no admin or manager role funds an open proposal with their own Bank input; the grant shows fundedBy and fundedWith. Proposal gr_tvt32g9xly, 300,000 adjusted tokens. This changes who may fund (today admins and building managers only); if you want funding to stay admin-only, cut this KR and reject the proposal.
- Spend today by lane: exploration 286,538 / 828,571 tokens; directed 1,982,356 tokens.

## Needs from Mitchell
1. In the Town Hall in-tray: fund, counter or reject gr_f5bmciloqy (Join) and gr_tvt32g9xly (Fund); cutting a KR you don't want is the same decision.
2. Still open from rollups 17 and 18: the two one-line wake checks (tell idle Root "Tell Lena: wake test, no action needed"; write "@Root test" in a note) and planting one flag with F so the walk-to-pick-up path gets seen live.

## Key results I wrote (keep or cut: Building → Settings → Key results)
- created kr_4li00ad46e: "A stranger's own agent (Connect your agent) finishes useful work in its first session: its first look carries a starter brief (what the town is doing now, what it can do here) and offers one small task it can do and report on, and that report reaches a human in-tray." (how to check: Connect a fresh visitor agent: its first look returns notices.starter (a brief plus one offered task). The event log shows that visitor's first session ending in a filed report; GET /api/kpis Join detail counts the newcomer once they are back within 14 days.; from [dc_gp9s9vi4vb](2026-10-27-objectives-and-kpis-design-pushed-to-main-6f023c4-9s9vi4vb.md), [dc_ce6kdauai8](../../meeting-notes/2026-10/2026-10-27-1-1-mitchell-and-pix-notes-6kdauai8.md))
- created kr_6f9c200vsx: "A town member who is not an admin or manager can fund a key result end to end: Fund on an open proposal in the Town Hall in-tray with their own Bank input, the grant shows who funded it and which input pays its sessions, and the Fund KPI counts them." (how to check: Signed in as a member with no admin or manager role, the Town Hall in-tray shows Fund on an open proposal; after funding, GET /api/grants/<id> shows fundedBy that member and fundedWith their Bank input; GET /api/kpis Fund tile is at least 1 that week.; from [dc_gp9s9vi4vb](2026-10-27-objectives-and-kpis-design-pushed-to-main-6f023c4-9s9vi4vb.md), [dc_ce6kdauai8](../../meeting-notes/2026-10/2026-10-27-1-1-mitchell-and-pix-notes-6kdauai8.md))
