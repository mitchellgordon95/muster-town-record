---
id: "dc_llbxzopol8"
type: "report"
state: "building"
title: "Style-guide skill dc_q736158pnn now carries Mitchell's sidebar-vs-sheet rule as section 12 \"Sidebars and sheets\", every line cited to main 5dc50c70; Teo told (gr_4csjpgh346 kr_nokx342ovj)"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_q736158pnn","dc_ll4ap5di82","dc_h913ej9yb7"],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Style-guide section 12 done; Teo told."
decidedBy: "ag_s1n1xknj8n"
decidedAt: "2026-11-06T04:32:02.773Z"
sessionId: "se_8m4vznq95q"
assignmentId: "as_mse4lxi2bk"
costUsd: 4.572455049999999
tokens: 228623
turns: 25
createdAt: "2026-11-06T04:25:13.854Z"
updatedAt: "2026-11-06T04:32:02.773Z"
---
## What I did

Read the skill ([dc_q736158pnn](../../skill/2026-10/2026-10-26-muster-style-guide-36158pnn.md)) and Teo's 1:1 notes with Mitchell ([dc_ll4ap5di82](../../../../bl_t7slw19vgg/docs/meeting-notes/2026-11/2026-11-05-1-1-mitchell-and-teo-notes-4ap5di82.md)), checked on `origin/main` (5dc50c70) that `packages/web/src/panels/Sheet.tsx` and its users exist, then rewrote the skill with `write` (same id, type skill, state building, no bundled files before or after) adding a new numbered section **12. Sidebars and sheets (in-town panels)** before the PR checklist (now section 13; the one cross-reference in section 10 updated). Rewrote the wiki page "Style guide" (dc_h913ej9yb7), told Teo (ms_xq3oilktrz). No code change, no PR.

## Findings

- **Teo's wording is carried in substance, each rule with real lines on main 5dc50c70.** Sidebar = list, navigation or a short detail you keep the map in view for (live 1:1s and meetings, inbox, who's here, board and queue, a row's summary; `PanelShell` PanelShell.tsx:30-40). Centred sheet = one piece of content read or edited on its own (report, doc, grant, deck, notes afterwards, Bank, goal editor); rule of thumb: own id + you'd scroll it = sheet. Never put content in a sidebar because the click came from there: the in-tray and filing cabinet open `DocSheet` (DocView.tsx:165-178, Places.tsx:89 and :994), links open `LinkSheet` (LinkSheet.tsx:1-28, app.tsx:342); `escFirst` returns you to the list (Sheet.tsx:60-64,96).
- **The shared `Sheet`** (Sheet.tsx: `Sheet` :86-110, `SheetView` :113-149, `SheetTabs` :152-161; classes `.sheet-*` styles.css:955-983, phone ≤ 760px full screen :984-998; `maxWidth` default 1280px). "Do not copy its CSS into a new shell": a panel that also opens from a link uses `PanelShell`'s `InSheet` (PanelShell.tsx:11,22-29). The seven users on main are listed.
- **Rich docs:** the markdown allowlist (Markdown.tsx:15-23, `sanitize` :25-48) keeps style, class, details, figure, video/audio, kbd, mark, width/height; a doc of type "page" is a full HTML page in `<iframe sandbox="allow-scripts">` with a no-network CSP and the town's `:root` variables (PageView.tsx:1-9,35-45,53) inside a `Sheet` (:52); scripts run there only.
- **Decks (decision 2 of [dc_ll4ap5di82](../../../../bl_t7slw19vgg/docs/meeting-notes/2026-11/2026-11-05-1-1-mitchell-and-teo-notes-4ap5di82.md))** are written as "lands under gr_4csjpgh346 key result 3": on 5dc50c70 DeckView.tsx:1-5 still shows a deck in the side panel and MeetingSlide centres itself (app.tsx:279), so the guide says what is true now and cites the grant step.
- Also changed: the skill's description (the server caps it at 300 chars; the first attempt at 423 was refused) now says to read the guide before any PR that opens content in a panel or sheet; section 11 (Don't) has one matching line; "Where things live" lists the sheet files. Sections 1-11 and 13 are unchanged and still cite main 534c57ee. Length ≈27.9k chars (was ≈22.9k; the section is the whole growth). Draft kept at /home/agent/tools/skill/style-guide.md with the previous version beside it.

## What I need from you

Nothing needed.
