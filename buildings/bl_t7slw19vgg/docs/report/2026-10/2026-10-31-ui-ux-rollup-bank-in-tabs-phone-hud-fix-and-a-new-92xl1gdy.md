---
id: "dc_5i92xl1gdy"
type: "report"
state: "building"
title: "UI / UX rollup: Bank in tabs, phone HUD fix, and a new \"no dead ids\" key result"
authorId: "ag_s1kuuuo54b"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":["dc_yztytjwzyo","dc_5nv9tk4z4j","dc_lfi124w5fs","dc_grclhet21i","dc_46tfl42ata","dc_4p133oialh","dc_5o3qs5czuy"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-31T20:00:07.630Z"
sessionId: "se_mg7jdm2hdi"
createdAt: "2026-10-31T19:54:52.071Z"
updatedAt: "2026-10-31T20:00:07.630Z"
---
Live: 49afcdd, which includes fa48254 and f402bcf.

## Shipped
**1. The Bank interior is now in tabs**
**What it is:** This is the redesign you asked for in 1:1 mt_ew2d0mm7h9. BankPanel is split into tabs, each tab has one object in the room, and the teller counter is gone. PR #119, merged at f402bcf ([dc_5nv9tk4z4j](2026-10-30-bank-in-tabs-one-room-object-per-tab-teller-counte-v9tk4z4j.md), topic page [dc_v4itjbkgfi](../../wiki/2026-10/2026-10-30-bank-interior-tabs-and-room-objects-itjbkgfi.md)). Four earlier attempts ended without a report ([dc_lfi124w5fs](2026-10-30-session-ended-without-a-report-message-from-mitche-i124w5fs.md), [dc_grclhet21i](2026-10-30-session-ended-without-a-report-redo-mitchell-s-int-clhet21i.md), [dc_46tfl42ata](2026-10-30-session-ended-without-a-report-retry-mitchell-s-ba-tfl42ata.md), [dc_4p133oialh](2026-10-30-session-ended-without-a-report-bank-interior-redes-133oialh.md)) before a fork finished it.
**What you'd see:** Walk into the Bank and click any object in the room: the panel opens on that object's tab. No picture was captured.
**Your call:** None

**2. The HUD no longer covers the map on phones**
**What it is:** This was mobile piece 3. At phone width the HUD card collapses, and you can tap a blocked badge to read why it's blocked. PR #106, merged at fa48254 ([dc_yztytjwzyo](2026-10-30-mobile-piece-3-hud-collapses-on-phones-blocked-bad-tytjwzyo.md)).
**What you'd see:** Open the town on a phone. The map is clear, and tapping a blocked badge opens its reason card. No picture was captured.
**Your call:** None

## Decided
- [dc_yztytjwzyo](2026-10-30-mobile-piece-3-hud-collapses-on-phones-blocked-bad-tytjwzyo.md) (mobile piece 3, HUD on phones) → approve
- [dc_5nv9tk4z4j](2026-10-30-bank-in-tabs-one-room-object-per-tab-teller-counte-v9tk4z4j.md) (Bank tabs, f402bcf) → approve
- [dc_lfi124w5fs](2026-10-30-session-ended-without-a-report-message-from-mitche-i124w5fs.md), [dc_grclhet21i](2026-10-30-session-ended-without-a-report-redo-mitchell-s-int-clhet21i.md), [dc_46tfl42ata](2026-10-30-session-ended-without-a-report-retry-mitchell-s-ba-tfl42ata.md), [dc_4p133oialh](2026-10-30-session-ended-without-a-report-bank-interior-redes-133oialh.md) (Bank redesign sessions that ended without a report) → handled; a fork finished the work in as_rybf4eodu2
- [dc_5o3qs5czuy](2026-10-31-exploration-61-of-recent-docs-show-ids-nobody-can-3qs5czuy.md) (exploration: 61% of the 200 newest docs contain an id nobody can click) → approve

## Key results
| Key result | Status | Spent / granted |
|---|---|---|
| kr_utx7pmv1yk "No dead ids": every id the town mints opens what it names (new, written from findings [dc_q669jtwr1i](../../note/2026-10/2026-10-31-findings-61-of-recent-town-docs-show-ids-nobody-ca-69jtwr1i.md)) | not-started; a grant is proposed | 0 / no grant yet |

Today's spend by lane: exploration 22,326 tokens (6,663,852 free under the goal), directed 0 tokens. I wrote kr_utx7pmv1yk this round, so you can keep it or cut it. The evidence behind it: in the 200 newest docs, about 570 mentions of as_/mt_/kr_/se_/ag_/mf_ ids are plain text, and only dc_ and gr_ ids are links.

## Needs from Mitchell
Nothing needed.

_Already waiting in your in-tray: 1 proposal (gr_seh9d840jo), 0 requests, 0 rollups._

## Key results I wrote (keep or cut: Building → Settings → Key results)
- created kr_utx7pmv1yk: "No dead ids: every id the town mints (as_, mt_, kr_, ag_, bl_, se_, mf_ as well as dc_/gr_) shows as a clickable link that opens what it names, labelled by name where known, in docs and in the agent and building panels." (how to check: Open any recent report on muster.town as a guest (e.g. a rollup). Every as_/mt_/kr_/ag_ id in it is a link that opens a panel. Re-running the count in [dc_q669jtwr1i](../../note/2026-10/2026-10-31-findings-61-of-recent-town-docs-show-ids-nobody-ca-69jtwr1i.md) finds 0 unlinked id kinds.; from [dc_q669jtwr1i](../../note/2026-10/2026-10-31-findings-61-of-recent-town-docs-show-ids-nobody-ca-69jtwr1i.md), [dc_fsi2uzw9ty](../../wiki/2026-10/2026-10-29-ui-ux-goal-and-key-results-i2uzw9ty.md))
