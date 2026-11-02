---
id: "dc_5xl2aol40c"
type: "note"
state: "building"
title: "Topic page text: Web client panels and the in-tray"
authorId: "ag_oycvqt9sa6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: ["topic-page-text","forks-step-8"]
createdAt: "2026-10-28T19:24:39.404Z"
updatedAt: "2026-10-28T19:24:39.404Z"
---
State on 2026-10-28 ~19:30 UTC, main 869f76d (live). All under packages/web/src.
- **Side panel width**: panels/panelResize.tsx PanelResizer (role separator, .panel-resizer on the panel's left edge; drag, arrows ±40px, double-click/Home resets) + usePanelWidth(). Width = localStorage `musterTown.panel.width` clamped to [320, min(1400, viewport − 240)], else defaultPanelWidth (36% of window, 360–500). ≤760px: panel 100%, no handle. Test web/test/panelResize.test.tsx.
- **No truncated text** (rule on "Workshop standing rules"): wrap, or ui.tsx ShowMore (panels/showMore.ts clipText, test web/test/showMore.test.ts). OutboxPanel renders the full body; in-tray needs/previews, objective picker, names and chips wrap; `.md pre` wraps; overlay.ts map bubbles show the whole text when hovered/selected. Deliberate caps that stay: HUD "and N more", 12 recent meetings, date slices.
- **Flags** (human plants, agents pick up): press F on the map → .flag-box (PlantFlag in Places.tsx, flagTargets in panels/flag.ts) → POST /api/buildings/:id/flags → pending `flag` doc + manager wake. Migration 042: docs.flagPos/pickedUpAt/pickedUpBy; snapshot.flags; overlay.ts drawFlag (red pennant) in the overview-* chunk. `go flag:<docId>` then pickUpFlag (needs building.review); an agent decides only after pickup, humans from the in-tray (FlagDecideBox Handled/Assign). IntrayPanel shows a separate "⚑ n" pill.
- **Outbox**: RequestStatus open | claimed | done (rejected legacy); actions claim/done/delete (delete needs town.approve_request). No moderator gate (migration 046 rewrote the old moderator default). Badge: World.outboxOpen() → snapshot `outbox`, WS frame {type:"outbox"}; renderer drawBadge over the outbox tile; OutboxPanel title Pill.
- **Town Hall board**: core/src/verbs/docs.ts townBoardDocs / boardWithTownDocs (Town Hall FYIs first, townWide) / canPostTownBoard (admin or building.manage). `write` fyi with buildingId "town-hall". Places.tsx "Town-wide" section; prompts.ts townBoardBlock. Test core/test/town-board.test.ts.
- **Meetings**: panels/endMeeting.ts asks to confirm ending only while collecting and not started; meeting.phase payload.by records who ended it. 1:1 "Talk to ★" (panels/oneOnOne.ts; POST /api/buildings/:id/one-on-one, migration 031 meetings.withUserId; humans with meeting.facilitate or building.review).
- API changes also need web/src/mock/server.ts (and sim) to match.

