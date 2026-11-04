---
id: "dc_nlel1q2s9n"
type: "report"
state: "building"
title: "Onboarding close rollup: gr_zoo2cf2zpp (join funnel counts real strangers) closed as done, all three key results live-checked in ad27e6f4; 24,769 tokens back to the Bank"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_i39wsqtnj4"],"urls":["https://muster.town/api/join-funnel"]}
tags: ["rollup","grant-close"]
verdict: "stop"
decision: "pending"
sessionId: "se_1zch50hl41"
assignmentId: "as_k7mcithq2c"
costUsd: 1.9701617999999999
tokens: 98508
turns: 19
createdAt: "2026-11-04T19:00:06.991Z"
updatedAt: "2026-11-04T19:00:06.991Z"
---
Live: **ad27e6f4** (server started 2026-11-04 18:57:28Z); it contains c5e0005a. This card closes one grant; the gr_a6512x0je1 checkpoint card filed minutes ago stands on its own. Findings behind the grant: [dc_dmmktg7x3w](../../note/2026-11/2026-11-03-findings-the-join-funnel-s-top-step-can-t-be-trust-mktg7x3w.md); building page [dc_mosy9yc4ht](../../wiki/2026-11/2026-11-04-join-funnel-top-steps-measure-real-strangers-gr-zo-sy9yc4ht.md).

## Shipped

**1. The join funnel now counts real strangers, not page loads or our own checks (gr_zoo2cf2zpp, closed as done)**
**What it is:** Three new funnel steps, one commit c5e0005a (migration 090, core join-funnel.ts, server app.ts and auth/routes.ts, web StatsPanel). `guestVisitors` counts a browser once per UTC day by a random id it keeps in its own localStorage (only its sha256 is stored, no IP, no login); `homeViews` does the same on the homepage; `signInStarted` counts a press of Sign in at GET /auth/github with no session, so a stranger who quits at GitHub's consent page still shows. Headless browsers and command-line tools (HeadlessChrome, curl, wget, Playwright, Puppeteer and the like) are never counted, so the building's own live checks stop inflating the funnel. 275,231 of 300,000 tokens spent; 24,769 returned to the Bank.
**What you'd see:** `curl https://muster.town/api/join-funnel` → today's workshop row. Live check from my desk at 18:57-18:58Z: five browser-UA pings with one visitor id took guestCardViews 371→376 and guestVisitors 0→1; pings with HeadlessChrome or curl's UA answered `{counted:false}` and changed nothing; two homepage pings with one id took homeViews 0→1; one GET /auth/github with a browser UA took signInStarted 0→1 with signIns still 0. Town Hall → User stats easel → E shows the columns Home, Saw card, Visitors, Pressed Sign in with a definition line saying headless browsers and command-line tools are not counted (served bundle main-72t9el_F.js carries both). No picture: the counts are API and the easel needs your admin session. Note that today's row now holds 5 views, 1 visitor, 1 home view and 1 sign-in press that are mine.
**Your call:** None. (The key results went to met on close; flip one to missed on the grant if the live checks don't convince you.)

## Decided
- [dc_i39wsqtnj4](2026-11-04-gr-zoo2cf2zpp-taken-whole-and-pushed-to-main-as-c5-9wsqtnj4.md) (c5e0005a pushed, live check parked) → approved earlier; its continuation (this session) did the live check and closed the grant.
- No other reports in the in-tray.

## Key results
| Grant | Key result | Status | Spent / granted |
|---|---|---|---|
| gr_zoo2cf2zpp (closed done) | kr_tsrsclo71o guestVisitors per day, headless skipped | met | 275,231 / 300,000 |
| gr_zoo2cf2zpp | kr_o5pvkvop0h signInStarted counted at Sign in | met | " |
| gr_zoo2cf2zpp | kr_wy2r43djiw homeViews + User stats columns with definitions | met | " |
| gr_fibsfwr4tz | kr_pxisdsocdp read-only guest asks to join | live, round trip pending | 407,049 / 450,000 |
| gr_fibsfwr4tz | kr_a32db87f39 guest card promises only Ask to join | live | " |
| gr_fibsfwr4tz | kr_fbef01cccb join funnel public and moving | live | " |
| gr_fibsfwr4tz | kr_4395ff116f pending request in HUD Notices with age | live | " |
| gr_fibsfwr4tz | kr_bf2df18aa1 real round trip once | waiting on a real stranger (outbox [dc_mgcbv3kqnd](../../../../../town-hall/outbox/2026-10/2026-10-31-one-real-join-round-trip-a-never-granted-github-ac-cbv3kqnd.md)); final check scheduled 2026-11-07 21:00Z | " |
| gr_a6512x0je1 (at checkpoint) | kr_6xv83q1k14 / kr_7pdn6k1w2r / kr_fk7c0pdvvs never-run collectives say so | on-track: 48d88720 is now live in ad27e6f4, live check held until the checkpoint is decided | 434,786 / 150,000 |

Spend today by lane: exploration 68,642 tokens (free under the goal 3,292,792); directed 151,656 tokens.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 0 proposals, 4 requests ([dc_mgcbv3kqnd](../../../../../town-hall/outbox/2026-10/2026-10-31-one-real-join-round-trip-a-never-granted-github-ac-cbv3kqnd.md), [dc_ulla3hu21p](../../../../../town-hall/outbox/2026-11/2026-11-01-add-on-to-the-join-round-trip-dc-mgcbv3kqnd-after-la3hu21p.md), [dc_fvlt8xajnz](../../../../../town-hall/outbox/2026-11/2026-11-02-add-on-to-the-join-round-trip-dc-mgcbv3kqnd-after-lt8xajnz.md), [dc_wtz7ltq8hf](../../../../../town-hall/outbox/2026-11/2026-11-03-add-on-to-the-join-round-trip-dc-mgcbv3kqnd-let-in-z7ltq8hf.md)), 1 rollup ([dc_wi034dm7du](2026-11-04-onboarding-checkpoint-rollup-never-run-collectives-034dm7du.md))._
