---
id: "dc_cv0n2rw5mp"
type: "report"
state: "building"
title: "One shared Sheet: the Bank and the goal editor open on it (PR #371, draft); parked on CI"
authorId: "ag_cltr75oifo"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: ["parked"]
verdict: "continue"
decision: "approve"
decisionNote: "Step 1 of gr_4csjpgh346 built (PR #371 draft, one Sheet for Bank + goal editor, no visual change, 342 tests green). Continuation as_1bk9eprvpf already waits on {pr:371} to mark ready and merge."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-05T20:39:09.701Z"
sessionId: "se_cc5lxfxom8"
assignmentId: "as_xapgn49yfp"
costUsd: 2.4510662000000005
tokens: 122553
turns: 46
createdAt: "2026-11-05T20:39:00.682Z"
updatedAt: "2026-11-05T20:39:09.701Z"
---
## What I did
Built one shared centred `Sheet` component and moved the Bank and the goal editor onto it (grant gr_4csjpgh346 step 1, kr_xnt1h13yce). Opened draft PR https://github.com/mitchellgordon95/muster-town/pull/371. I'm parked until its CI finishes.

## Findings
- **What's new:** `packages/web/src/panels/Sheet.tsx` has three parts:
  - `Sheet`: draws the backdrop over the map, closes on a backdrop mousedown or Esc, and leaves room on the right for the side panel.
  - `SheetView`: the sheet without the backdrop, for tests.
  - `SheetTabs`: the tab column.
- **How it's used:** a caller gives the sheet its head, optional tabs, the main column and an optional side column behind a draggable divider. The divider's width is saved per sheet. If main and side share state, the caller can lay out both columns itself (`columns(divider)`, which the Bank uses). On a phone the sheet stacks as one scroll or as a 40/60 split. The full list of props is on the topic page [dc_cfyhhhf9c0](../../wiki/2026-11/2026-11-05-sidebars-and-sheets-gr-4csjpgh346-yhhhf9c0.md).
- **Old shells removed:** the `.ge-wrap/.ge/.ge-head/.ge-body/.ge-tree/.ge-divider/.ge-detail` and `.bank-wrap/.bank-sheet/.bank-head/.bank-body/.bank-tabs/.bank-tab/.bank-cols/.bank-main/.bank-side/.bank-divider` classes are gone, and git grep finds none of them in web/src. In their place is one `.sheet-*` block. Inner classes stay (`.ge-tag`, `.ge-tools`, `.bank-note`, …), and the Bank's sidebar text rules are now `.bank-about`.
- **One divider:** `GeDivider` and the Bank's copy of it became one `SheetDivider` (panelResize.tsx). Saved widths keep their old localStorage keys, so nobody's layout resets.
- **The census script** (scripts/disclosure-census.mjs) now finds the new class names.
- **Tests:** typecheck passes, `check:css` passes (0 stray values), and all 342 web tests pass.
- **No visual change:** I took screenshots in the mock before and after the change, at 1280×800 and 390×844:
  - All 5 Bank tabs are pixel-identical, apart from ≤74 px of changing numbers.
  - The goal editor's layout is the same. One line of text wraps differently, and on the phone a 1 px border moved from the bottom of the tree to the top of the detail.
- **Interactions checked:** dragging the divider works on both sheets (Bank side 385→535 px, goal detail 495→645 px, and the widths were saved). Double-click resets it. A click inside doesn't close the sheet; Esc and a backdrop click do.
- **Esc quirk (not from this change):** in the mock, if the map's building tour is active when the page loads, it takes the first Esc (MapCanvas calls stopImmediatePropagation). That is already on main. It only showed up because test timing differed.
- **Pictures for the rollup:** mf_m8ve20l835 (Bank) and mf_mjkwtjkwx7 (goal editor), both from the mock at 1280×800.
- **Topic page:** I rewrote [dc_cfyhhhf9c0](../../wiki/2026-11/2026-11-05-sidebars-and-sheets-gr-4csjpgh346-yhhhf9c0.md) with the Sheet's props and how steps 2–5 should use it.

## What I need from you
Nothing needed.
