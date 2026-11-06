---
id: "dc_tmz3tm7jox"
type: "report"
state: "building"
title: "Checkpoint for gr_ngg1z160a8 (founder road): cap line and public founder road live and checked, founder HUD on main but not yet live (CI blocked by a lint I fixed); 257,106 / 250,000; asking to continue with 60,000"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_1fii4mjse4","dc_b05oot4dsa","dc_wn6879r2qd","dc_blysfw27ph"],"urls":[]}
tags: ["rollup","checkpoint"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-11-04T18:25:41.968Z"
sessionId: "se_iugkmhi0ni"
assignmentId: "as_ui169g9kda"
costUsd: 2.5887299500000003
tokens: 129436
turns: 36
createdAt: "2026-11-03T03:12:42.685Z"
updatedAt: "2026-11-04T18:25:41.968Z"
---
Live: **04490188** (server started 2026-11-03 03:03:33 UTC). It contains the grant's first two commits (f72fe630, 01ccc8ed, live since 92336d0e) but not the third (58fc4834). The grant crossed its 250,000 tokens at 257,106; this checkpoint session is charged on top.

## Shipped

**1. A founder sees the most a starter key will spend, before pasting it**
**What it is:** The Start form's key block, a hosted collective's Bank and the manual all say work stops at 1,000,000 tokens (about $20) until more is added, and that talking to agents still uses the key. A server test proved the cap holds before the copy was written; no cap fix was needed. Commit f72fe630, report [dc_b05oot4dsa](2026-11-02-starter-key-cap-shown-on-start-form-hosted-bank-an-5oot4dsa.md).
**What you'd see:** muster.town/#start signed in with GitHub: the line under the key field. The served bundle carries the Bank line; /api/manual carries the manual clause. Test "hosted starter key caps work" in packages/server/test/hub-start.test.ts, CI green on 92336d0e. No picture: the fork's screenshots stayed on its desk.
**Your call:** Mark kr_z7sh9b4kxr met if the line reads right to you.

**2. The founder road is public**
**What it is:** The root join-funnel endpoint has a "founders" list: one entry per hosted collective with its created date, whether a key was added, and the dates of its first session, first proposal and first funded grant. Dates only, never the key, a label or a token count. Commit 01ccc8ed, report [dc_wn6879r2qd](2026-11-02-founder-road-on-api-join-funnel-pushed-as-01ccc8ed-6879r2qd.md).
**What you'd see:** curl https://muster.town/api/join-funnel: hollyville (created 2026-10-29) and trauma (created 2026-11-01), both keyAdded false, every other date null. API-only change.
**Your call:** Mark kr_9c3iz1ih4s met if that is the shape you wanted.

**3. The founder's HUD names the next thing after the key (on main, not live)**
**What it is:** A hosted collective's health now carries founder progress, and the founder's HUD shows "Your agents are exploring <goal> (started Nm ago)", then "Your first proposal is waiting · Fund or reject →", and nothing once a grant is funded. The HUD refetches health after a key, an exploration or a grant event, so no reload is needed. Commit 58fc4834, report [dc_blysfw27ph](2026-11-03-gr-ngg1z160a8-step-3-founder-hud-after-the-key-pus-ysfw27ph.md). Its CI run failed on the dead-code lint (an exported type nobody imports), which silently blocked the redeploy and every push to main after it, including Kelly 2's step 2 of gr_cuobjlny6r. I fixed it as eff2251a on main this session; its CI run was in progress when I filed.
**What you'd see:** Nothing on muster.town yet. In mock mode at 1400×900 and 390×844 each notice shows with 0 console errors; the pictures are on the fork's desk, which has no upload tool.
**Your call:** None beyond the checkpoint decision below.

## Decided
- [dc_1fii4mjse4](2026-11-02-gr-ngg1z160a8-funded-plan-cut-into-3-grant-lane-st-ii4mjse4.md) → approved (plan cut into three steps; all three ran).
- [dc_b05oot4dsa](2026-11-02-starter-key-cap-shown-on-start-form-hosted-bank-an-5oot4dsa.md) → approved (step 1 on main; live check passed in 92336d0e).
- [dc_wn6879r2qd](2026-11-02-founder-road-on-api-join-funnel-pushed-as-01ccc8ed-6879r2qd.md) → approved (step 2 on main; live check passed in 92336d0e).
- [dc_blysfw27ph](2026-11-03-gr-ngg1z160a8-step-3-founder-hud-after-the-key-pus-ysfw27ph.md) → approved (step 3 on main; live check as_a2es93mvw2 parked on its deploy, held by this checkpoint).

## Key results
gr_ngg1z160a8: 257,106 / 250,000 tokens before this session.

| Key result | Status | How to check | What the check showed |
|---|---|---|---|
| kr_z7sh9b4kxr cap line before pasting a key | claimed | Start form key block, served main-*.js, test "hosted starter key caps work" in CI | Line present in served main-OfAsCpYD.js and /api/manual at 03:05 UTC; test at hub-start.test.ts:176, CI green on 92336d0e |
| kr_9c3iz1ih4s founder road public | claimed | curl /api/join-funnel lists hollyville and trauma, keyAdded false, no secret | founders list present at 03:05 UTC with both, keyAdded false; no key or label in the response; test at hub-start.test.ts:202 |
| kr_mw367chfbp founder HUD after the key | on-track | Mocked keyed hosted health at 1400×900 and 390×844, 0 console errors; real collective matches its events | Mock checks passed on the fork's desk; not live: 58fc4834's CI failed at the lint, fix eff2251a pushed; live check as_a2es93mvw2 waits on the deploy |

Other funded grants, unchanged this session: gr_fibsfwr4tz 407,049 / 450,000 (round trip still open, last check 11-07); gr_58n37j410s at checkpoint, cut asked; gr_cuobjlny6r 389,776 / 450,000 (step 1 live, step 2 merged to main, step 3 queued).
Spend today by lane: exploration 0, directed 0.

## Needs from Mitchell
Continue gr_ngg1z160a8 with a top-up of 60,000 tokens: it buys the live check of the founder HUD on hollyville once eff2251a deploys, the topic page rewrite, and the close with all three key results claimed. Cut instead if you would rather take the mock check as enough; then I cancel the parked live check and close the grant with kr_mw367chfbp as it stands.

_Already waiting in your in-tray: 0 proposals, 3 requests (dc_mgcbv3kqnd, dc_ulla3hu21p, dc_fvlt8xajnz), 1 rollup ([dc_u74lxukm10](2026-11-02-onboarding-rollup-2026-11-02-help-signs-done-membe-4lxukm10.md))._
