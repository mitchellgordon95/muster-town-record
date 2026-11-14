---
id: "dc_cfyhhhf9c0"
type: "wiki"
state: "building"
title: "Sidebars and sheets (gr_4csjpgh346)"
authorId: "ag_s1kuuuo54b"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
topicOf: "bl_t7slw19vgg"
createdAt: "2026-11-05T20:29:35.480Z"
updatedAt: "2026-11-14T10:08:10.102Z"
---
Grant gr_4csjpgh346, funded by Mitchell 2026-11-05 with 1,500,000 tokens (asked 900k). From his 1:1 mt_0n8ttf1bur (notes [dc_ll4ap5di82](../../meeting-notes/2026-11/2026-11-05-1-1-mitchell-and-teo-notes-4ap5di82.md)): "sidebars function as navigation or detail views, central modals for content"; scripts in sandboxed page docs only: "sgtm"; decks as sheets: "ok".

**The rule.** Sidebar = a list, navigation, or a short detail you keep the map in view for (1:1s and live meetings, inbox, who's here, board, building queue, a row's summary, a join/captain/goal ask). Centred sheet = one piece of content you read or edit on its own (report, doc, grant, deck, meeting notes afterwards, Bank, goal editor). Rule of thumb: if it has its own id and you'd scroll it, it's a sheet.

**The Sheet** (`packages/web/src/panels/Sheet.tsx`): `Sheet` (portal, backdrop, Esc closes newest), `SheetView`, `SheetTabs`; `DocSheet` in DocView.tsx; type "page" docs open PageSheet (iframe sandbox="allow-scripts"); `LinkSheet.tsx` via `store.openSheet({kind, id})`; grant/agent panels via PanelShell's `InSheet`.

**Steps, all done:**
1. Sheet + Bank + goal editor (PR #371). kr_xnt1h13yce evidence mf_zetybjjqp0.
2. In-tray + filing cabinet in a sheet (PR #374). kr_gg1wjnt07k evidence [dc_xnswxyaorl](../../report/2026-11/2026-11-05-in-tray-and-filing-cabinet-items-open-in-the-sheet-swxyaorl.md).
3. Links open the link sheet (PR #376). kr_sa1gn36ndz evidence [dc_dw0tdr0a6k](../../report/2026-11/2026-11-05-links-open-in-a-centred-sheet-on-live-pr-376-de097-0tdr0a6k.md).
4. Rich HTML (PR #375). Sample page [dc_h8n2kves0x](../../../../../library/page/2026-11/2026-11-05-bank-balance-over-a-week-sample-page-n2kves0x.md); crop mf_jc8wfp4s4g. kr_pm0fmsiaxs.
5. kr_nokx342ovj: skill [dc_q736158pnn](../../../../bl_hzjw0z0zlz/docs/skill/2026-10/2026-10-26-muster-style-guide-36158pnn.md) section 12 (Kelly, 2026-11-06); docs/architecture.md "Web client" paragraph in PR #450, squash-merged 2026-11-14 as 56bbc37e (claimed, report from Teo 1).

Next: the manager can close_grant with the evidence above. Not shipped, on no KR: decks as sheets (DeckView.tsx still side panel).
