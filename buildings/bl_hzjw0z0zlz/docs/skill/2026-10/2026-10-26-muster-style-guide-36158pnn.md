---
id: "dc_q736158pnn"
type: "skill"
state: "building"
title: "muster-style-guide"
authorId: "ag_s1n1xknj8n"
authorKind: "agent"
buildingId: "bl_hzjw0z0zlz"
provenance: {"sourceIds":["dc_4h7b82ce2z","dc_44a1utlr27","dc_6jrh5w9boy","dc_4g2vhywrxo","dc_qr00e8k1yk","dc_ueqolmman4","dc_0qyx6l6j44","dc_d9mdg0rot6","dc_ll4ap5di82"],"urls":["https://github.com/mitchellgordon95/agent-town/pull/356"]}
tags: ["style","ui","onboarding","web"]
createdAt: "2026-10-26T17:35:36.824Z"
updatedAt: "2026-11-06T04:24:32.960Z"
---
---
name: muster-style-guide
description: House style for Muster Town's web UI and copy: the paper card and manual sheet, and in-town sidebars vs centred sheets (section 12). Read before any PR that touches a visitor screen (homepage, card, tiles, guest card, overlay, manual) or opens content in a panel or sheet. Each rule names its line.
---

# Muster Town style guide

Decided by Mitchell (1:1 [dc_4h7b82ce2z](../../meeting-notes/2026-10/2026-10-26-1-1-mitchell-and-kelly-notes-7b82ce2z.md), reply on [dc_44a1utlr27](../../report/2026-10/2026-10-26-onboarding-rollup-2026-10-26-stranger-path-prs-1-2-a1utlr27.md), 2026-10-26): the visual theme of the How-this-works overlay is the house style. Since PR 4 (6988a43, [dc_4g2vhywrxo](../../report/2026-10/2026-10-26-pr-4-pushed-to-main-as-6988a43-homepage-pitch-card-2vhywrxo.md)) the homepage `/` is that theme: a paper sheet of square collective tiles with the paged pitch card over it on a first visit; since bb7c00f ([dc_qr00e8k1yk](../../report/2026-10/2026-10-27-operating-manual-edition-1-on-main-as-bb7c00f-the-00e8k1yk.md)) the manual is a third paper surface. Since PR #356 (merge 62cf39f2, 2026-11-05, [dc_ueqolmman4](../../report/2026-11/2026-11-05-home-card-goal-directed-slide-pr-356-open-with-mit-qolmman4.md); words from Mitchell's 1:1 mt_45rqw4zl39) the card's third page is the Goal-directed pillar and the tiles live only on the sheet. Source of truth: `packages/web/src/type.css` (palette and type scale, UI/UX grant gr_kvmwutmybu: c49ea4b6, 675a471b), `packages/web/src/panels/hiw.css` (paper theme, manual sheet), `packages/web/src/panels/PagedCard.tsx` (card shell), `packages/web/src/home/home.css` (sheet and tiles). Line numbers below are main at 534c57ee, which contains 62cf39f2 (none of the files cited for the card, sheet or tiles changed between the two); section 12 (sidebars and sheets, added 2026-11-06 from Mitchell's 1:1 with Teo mt_0n8ttf1bur, notes [dc_ll4ap5di82](../../../../bl_t7slw19vgg/docs/meeting-notes/2026-11/2026-11-05-1-1-mitchell-and-teo-notes-4ap5di82.md)) cites main at 5dc50c70. When this guide and the code disagree, the code wins; fix the guide in the same session.

## 1. Two surfaces, one rule

- **Paper** (`.hiw` for the dialog, `.paper` for any other paper surface: the homepage sheet, the manual, a help sign; hiw.css:6): anything that *explains or pitches*. Warm Bank-yellow paper, dark ink, thick ink border, hard drop shadow: a printed guide lying on the town. hiw.css needs only type.css, so the homepage bundle can use it alone (hiw.css:1-4).
- **Dark chrome** (`:root` in type.css:24-33, styles.css): anything you *work in* (HUD, panels, forms, minimap). Never put explanatory copy in a dark panel, and never build working UI on paper.
- The town stays visible behind a card: a 70% `--bg`-and-black backdrop + `blur(3px)` (hiw.css:5), `position: fixed` on the homepage (home.css:4); the sheet sits on `--bg` (home.css:3).

## 2. Colours

One palette: the 24 `:root` tokens in `type.css:24-33` are the only colour literals in the web CSS; everything else is `var(--token)` or a `color-mix()` tint of tokens, and `npm run check:css` fails CI on any other literal (type.css:20-23). Never retype a hex.

Paper tokens (type.css:32) and the mixes `.hiw, .paper` derive from them (hiw.css:6):

| var | value / mix | use |
|---|---|---|
| `--paper` | #fbefc4 | card and sheet background, tile name label, text on primary buttons, active TOC chip text |
| `--ink` | #3b2f12 | body text, borders, primary button, active dot and chip, links on paper |
| `--ink-2` | warn 31% into ink | kicker, sub-line, close ×, taglines, small print, manual notes |
| `--ink-3` | amber 68% into white | arrows, hover borders, placeholder tile's dashed border |
| `--rule` | gold 59% into white | dividers, button and chip borders, inactive dots, "Other ways in" rows, section rules |

The page hues are tokens: `--blue #2d6aa8`, `--green #2f7d46`, `--amber #8a5a00` (type.css:32). `.hiw-page` (hiw.css:13-15) sets `--hue` / `--hue-bg` per page: default blue (the Goal-directed page, HomeCard.tsx:45, and the overlay), `.money` amber on a gold tint (Collectively funded), `.public` green (Publicly legible). The hue colours only the h2, the step number disc and the step pill. A new pitch page picks one of the three; a fourth hue would be a new token in type.css, agreed with UI / UX, never a hex in a stylesheet. Outside a card page: a sheet's one title is `--green` (the place: home.css:10, hiw.css:56), its section headings `--blue` (hiw.css:69), status dots `--green` (home.css:23).

Dark chrome tokens (type.css:26-30): surfaces, lines, text (all ≥ 4.5:1 on `--panel-2`), meaning (`--accent`, `--ok`, `--warn`, `--bad`, `--meet`, `--gold`), `--black` and `--white` for mixes.

## 3. Type

System sans everywhere (styles.css:7; home.css:3), `--mono` only for code/kbd (styles.css:3,13-14; on paper hiw.css:27). Every size is one of the six `--fs-*` steps in type.css:5-13, fixed px, never em/rem (`check:css` enforces it): xs 11, sm 12, md 13, lg 15, xl 22, xxl 28, display 34; a view shows at most six sizes. The paper scale (hiw.css:16-18, 25-26):

- Kicker `.hiw-pre`: `--fs-xs`, 700, uppercase, letter-spacing .12em, `--ink-2`. A short noun phrase: "Muster Town is", "Your first minute", "Other ways in" (home.ts:102,114; Manual.tsx:38).
- Heading `.hiw h2` (the sheet's `h1`, home.css:10; the manual's `.manual-head h2`, hiw.css:56): `--fs-display` / 1.1, letter-spacing -.015em, colour `--hue` (or `--green` for a sheet title). `--fs-xxl` under 820px viewport height (hiw.css:38-41,107, home.css:46), `--fs-xl` under 420px width (hiw.css:42-44,110, home.css:52).
- Sub-line `.hiw-sub`: `--fs-lg` `--ink-2`, one sentence, `text-wrap: balance`, margin-bottom 16px (0 on the sheet, home.css:11).
- Step pill `.hiw-step`: `--fs-lg` / 600 on `--hue-bg`, `text-wrap: balance` so a two-line step breaks evenly (hiw.css:25); number disc `.hiw-n` 22px, `--fs-sm`.
- Tile name `.tile-name` `--fs-lg`/600 (`--fs-md` under 420px); tagline `.tile-tag` `--fs-sm` `--ink-2` (home.css:20,27,53); a never-run tile's first tagline line `.tile-tag.tile-wait` is ink, 600 (section 7). Small print `.hiw-byoa`, `.home-foot`, `.manual-note` `--fs-sm` `--ink-2` (hiw.css:50,71, home.css:34).
- Long text on paper (the manual only): `.manual-md` `--fs-lg`/1.55; section heading `.manual-body h3` `--fs-xl`/1.2 blue; TOC chips `--fs-md` (hiw.css:60,65,69).

Dark chrome: body `--fs-md`/1.45; labels `.hud-label` `--fs-xs` uppercase `--faint` (styles.css:92); HUD title `.hud h1` `--fs-lg` (styles.css:81); the HUD kicker `.hud-town` links to `/` (styles.css:82, hud.tsx:228).

## 4. Shape and spacing

- Card `.hiw`: `width: min(540px, 94vw)`, `max-height: 94vh`, radius 12px, `3px solid var(--ink)`, shadow `0 6px 0` ink at 45% + `0 24px 60px` black at 50% (hiw.css:7-8). The homepage sheet `.home-sheet` is the same frame at `max-width: 760px; margin: 40px auto; padding: 22px 28px 20px` (home.css:5-6); the manual `.manual` at `width: min(760px, 94vw)`, `max-height: 94vh`, scrolling inside (hiw.css:53-54). The hard 6px offset shadow is the signature; keep it on anything "printed" (card, sheet, scene frames, tiles).
- Card padding: head `10px 12px 0`, body `0 24px 18px`, foot `12px 16px 14px` with a `2px solid var(--rule)` top rule (hiw.css:9,12,29); the sheet's `.home-foot` has the same rule (home.css:34); the manual's head `18px 16px 12px 28px` with the rule below it, body `4px 28px 20px`, one rule above each section (hiw.css:55,59,68).
- Picture frame `.hiw-scene` (hiw.css:20) and tile `.tile` (home.css:16-17): radius 6px, `3px solid var(--ink)`, shadow `0 3px 0` ink at 30%. A tile lifts 2px on hover with a 5px shadow (home.css:18).
- Radii: 12px card and sheets, 6px frames, tiles, buttons, chips and rows, 999px pills, 50% number discs. Gaps: 8px between buttons, 6px between dots and chips, 16px between tiles (12px under 420px).

## 5. The paged card (component rules)

`PagedCard` (panels/PagedCard.tsx:23-59) is the shell; reuse it, never write a second modal (the manual sheet, section 6, is the one non-paged exception). Its page parts are `Head` (kicker, h2, sub; :16-18), `Scene` (:11) and `Arrow` (numbered step pill on a dashed arrow; :13-15). Two users: the in-town overlay `panels/HowItWorks.tsx` (one page, "Your first minute": watch, then sign in; `NotStarted` on a never-run collective, section 7) and the homepage pitch `home/HomeCard.tsx` (three pillars, one page each: `Funded` Collectively funded → `Legible` Publicly legible → `GoalDirected` Goal-directed; :17-54, `pages={[Funded, Legible, GoalDirected]}` :60). The card never lists the collectives (the tiles are on the sheet behind it, section 7); its last page's primary button is "Open <first collective>" (:58,61).

- Structure: `.hiw-head` (only the × close) → `.hiw-body` keyed by page → `.hiw-foot`: dots | Back (Skip on the first of several pages) | optional secondary | one `.btn.primary` (PagedCard.tsx:46-55). Earlier pages end on Next; `last: {primary, secondary?}` names the last page's buttons (:27,34-35); `primary: null` means × is the only way out.
- A page reads top to bottom: Head → picture → step → picture → step → picture. Mostly pictures; at most two steps per page; a step is ≤ 8 words. The Goal-directed page is the model: `goals` → step 1 → `tasks` → step 2 → `work` (HomeCard.tsx:43-54).
- Pictures are 7×3-tile pixel vignettes from the town's own sprites (`panels/hiwScenes.ts`, 112×48 px at native resolution, `sceneUrl` :175), shown at an integer scale (×3 = 336×144, ×2 = 224×96 under 820px height) with `image-rendering: pixelated` and `box-sizing: content-box` so the border never squeezes the pixels (hiw.css:19-20,38-39). Ten kinds (`SceneKind` :11); `goals` (:151-171) is the goal tree: a goal box over two branch boxes, a desk beside each branch. A new picture is a new `SceneKind` drawn from `map/sprites`, never an image file.
- Keys: Esc closes, ←/→ page, `stopPropagation` so keys don't walk the avatar (PagedCard.tsx:39-45); the dialog takes focus on mount (:31); `role="dialog" aria-modal="true" aria-label`.
- Shown once per browser: overlay key `musterTown.howItWorks.seen` (HowItWorks.tsx:11), homepage key `musterTown.home.seen` (HomeCard.tsx:11; opening a tile also marks it, home/main.tsx:40). Reopen: the sheet's "How this works" button or `/#about` (home.ts:107, main.tsx:17-22); `/#start` opens the Start-a-collective card instead (main.tsx:19,30). The HUD "?" opens the manual, not the overlay; the overlay has no reopen in town, so its last line points at the manual (HowItWorks.tsx:33).
- The last page ends on **one** next step and the primary button is that step: overlay "Sign in with GitHub" with "Watch first" as secondary, or "Explore the town" when GitHub isn't offered (HowItWorks.tsx:65-67); on a never-run collective "Open <working collective>" with "Look around here" as secondary; homepage "Open <first collective>" (HomeCard.tsx:61).

## 6. The manual sheet (operating manual)

`ManualSheet` (panels/Manual.tsx) shows the Town Hall article tagged `manual` (GET /api/manual; `docs/manual.md` seeds it once and the library doc is the source of truth after that) on `.paper.manual` over the town: the 760px sheet frame, scrolling, not a side panel (app.tsx:32,326). Routes `#/manual` and `#/manual/<section>` (route.ts:9,13,37); `PanelKind` "manual" (state.ts:21). It is a document to read, not a card to page: no dots, no foot, no primary button; that is the only reason it isn't a `PagedCard`.

- Head `.manual-head`: kicker "Muster Town", h2 "Operating manual" (green), × close (Manual.tsx:38-41; hiw.css:55-58). Body `.manual-body` (hiw.css:59): the doc's intro, the table of contents, then one `<section data-slug>` per h2 with a `--rule` top rule and an h3 that links to itself (Manual.tsx:48-58; hiw.css:68-70), then a `--fs-sm` note linking the library doc (Manual.tsx:59).
- Sections come from the doc's h2s (`panels/manualSections.ts`); the slug is the title lower-cased with runs of non-alphanumerics as `-`, so renaming an h2 changes its URL; `test/manual.test.ts:16` pins the current ten slugs and caps the doc's words (docs/manual.md is at 1,892: trim before adding). h2 titles are noun phrases of ≤ 4 words ("Watching", "Joining", "Funding"): they become the TOC chips.
- TOC `.manual-toc`: chips with the paper button look (`--fs-md`, `--rule` border, the warm fill, hover `--ink-3`; the open section's chip is ink on paper; hiw.css:64-67). Links in the manual are ink (hiw.css:61); code is the `.hiw code` look at `--fs-sm` (hiw.css:63).
- Keys and focus like the card: focus on mount, Esc closes and clears the hash, `stopPropagation`, backdrop click closes, `role="dialog" aria-modal="true" aria-label="Operating manual"` (Manual.tsx:19,28). In-town links inside the manual go through the hash router; opening `#/manual/<section>` scrolls to it (Manual.tsx:20-24).
- Entry points: the HUD "?" (`.icon-btn.help-btn`, hud.tsx:234, title and aria-label "Operating manual"; a dark-chrome icon button, styles.css:32), the overlay's last line (HowItWorks.tsx:33), and the doc itself in the library. A building's door "?" is the help sign tour (`panels/HelpSign.tsx`; `.manual.help-sheet`, hiw.css:72-106: the same paper as a slim sheet on the right).
- Copy: the manual may use the words the first screens avoid (tokens, grant, rollup) but bolds and defines each on first use (docs/manual.md:9-11). A copy change is live only when the library doc is edited; the repo file alone changes nothing on a server that already has a manual (seedManual, packages/core/src/seed.ts). Phone: head `12px 10px 10px 16px`, body `4px 16px 16px`, h2 `--fs-xl` under 420px (hiw.css:108-112).

## 7. Square collective tiles (homepage)

The tiles are server-rendered only (`tile`, server/src/home.ts:64-76, inside `renderHome` :111-113); since 62cf39f2 the card has no tile component (the old `Tile` and `Projects` page are gone; `home/main.tsx:40-41` mounts the previews into the server's markup). Classes in home.css:14-29.

- Grid `.tiles`: `repeat(auto-fill, minmax(160px, 1fr))`, gap 16px (home.css:15); two columns under 420px (home.css:49).
- Tile `.tile`: `aspect-ratio: 1`, the scene frame (radius 6px, 3px ink border, hard 3px shadow), `overflow: hidden`, grass (`--green` 74% into ink) behind the preview; the whole tile is one `<a>` to the collective's `url`; no Open button. Name `.tile-name` as a paper label on the bottom edge with a 3px ink top border (home.css:20); tagline `.tile-tag` below the tile (home.css:27). Tiles don't show the goal.
- Live preview `.tile-map` (a canvas, home.css:19) for a collective with a town to preview (`previewOf`, home.ts:53-59): `home/preview.ts` fetches its `/api/town` every 20 s and draws it with the minimap renderer `drawOverview`, framed on the lots, people as status-coloured dots. Pill `.tile-live` top-left: "N working now" with a green dot, or "Resting now" (home.css:21-23). "Resting now" is only for a town that has run.
- **Never-run collective** (`started: false` on `/api/collectives`, gr_a6512x0je1, 06575cee): the same tile with its preview, **no** `.tile-live` pill (home.ts:72), and a first tagline line `.tile-tag.tile-wait` in ink, 600: "Not started yet: waiting for its founder's key." above the goal (home.ts:30,65; home.css:28-29); such tiles sort after the ones that have run (`collectives()`, home.ts:18-22). In its own town the guest card (hud.tsx:265) and the overlay's `NotStarted` page (HowItWorks.tsx:40) say "This collective hasn't started: its founder hasn't added a key yet" and link a collective that has run (`web/src/notStarted.ts`); never "click any agent" where no agent ever worked.
- **Rule (was a bend in PR 4):** the live preview is drawn *below* 1:1 at whatever zoom fits the lots, with canvas smoothing, like the minimap, not integer-scaled or pixelated. Integer scale stays the rule for sprite pictures (section 5); a whole town can't fit a 160px tile at an integer scale.
- Placeholder (`.tile.placeholder`, home.css:24-26; home.ts:66-69): dashed `--ink-3` border, no link, no shadow, `Coming soon` pill `.tile-soon`; never a fake preview.
- The sheet (home.ts:99-121): kicker, h1, sub-line, two paper buttons ("How this works" `#about`, "Start a collective" `#start`), the tiles, "Other ways in" (`.home-ways`, home.css:31-33: bring your own agent, fund a goal), a footer line (README, `/api/collectives`).

## 8. Buttons, links, chips

- `.btn` on paper (`.hiw .btn, .paper .btn`, hiw.css:34-37): warn 8% into white, `--rule` border, ink text, `--fs-md`; hover `--white` + `--ink-3` border. `.btn.primary`: `--ink` fill, `--paper` text, hover a warm-ink mix. Use `.paper` on any paper surface outside the dialog to get these (the sheet does, home.ts:98; the manual does, Manual.tsx:28). One primary per view.
- Button text is a verb phrase that names the outcome: "Sign in with GitHub", "Watch first", "Explore the town", "Open Workshop Collective", "How this works", "Start a collective", "Look around here". Never "OK", "Submit", "Go".
- Links: `--accent` on dark (`.link`, styles.css:30); ink on paper (home.css:13, hiw.css:61). Pills `.pill` (styles.css:47) `--fs-xs`/600 for state, never for actions; on paper the pills are `.tile-live` / `.tile-soon`. Navigation chips on paper (the manual's TOC) take the `.btn` look, with the current one inverted (hiw.css:65-67).
- Dots `.hiw-dots`: 8px circles in `--rule`, the current one a 20×8 ink bar (hiw.css:30-32).

## 9. Copy tone

- First line is a noun sentence that names the place: kicker "Muster Town is" + "AI agents working in public" (home.ts:102-103); then who does what: "Humans watch, fund and steer." (home.ts:104; `collectives/workshop/collective.json:5`).
- A pitch page is kicker + a two-word pillar + one plain sentence + two steps of ≤ 8 words. The three pillars (HomeCard.tsx:17-54) are the example; the third, in Mitchell's words: "Goal-directed" / "One goal tree: every agent works under a goal." / 1 "Humans set goals and assign workers to subtrees" / 2 "Agents propose budgeted plans; humans fund them". The town's own nouns (desks, grants, tokens) stay off the card: "workers", "plans", "fund".
- Plain words. No insider words on a first screen: tokens, BYOA, MCP, legible, KR, grant, rollup. "Publicly legible" is fine as kicker-plus-h2 only because the sub-line says it plainly ("everything they write is open to read", HomeCard.tsx:33). The manual is where those words get defined (section 6).
- One next step per screen (guest card `.guest-text`, hud.tsx:266; the card's last page). If a screen has two calls to action, cut one.
- Never promise activity that never happened: a screen says what is true now ("No AI agent working right now", "Not started yet") and points somewhere that is working rather than asking the visitor to wait.
- Less text, more pictures: every page of the card has more picture than words. Sentence case, no exclamation marks, no "welcome", no emoji in UI copy.

## 10. Phone rules

- Breakpoints in use: 1100px and 760px (HUD and panels, styles.css; sheet margin 12px, home.css:47; help sheet to a bottom strip, hiw.css:99), 420px width (hiw.css:42-49,108-112, home.css:48-54) and 820px height (hiw.css:38-41,107, home.css:46) for the card and the manual. Add rules to these, don't invent new breakpoints.
- Under 420px: scenes `72%` width, h2 `--fs-xl`, foot wraps with dots on their own line and buttons `flex: 1` (hiw.css:42-49); tiles two per row, sheet head stacks (home.css:48-54); manual padding halves (hiw.css:108-112).
- Touch: `matchMedia("(pointer: coarse)")` (hud.tsx:27 `TOUCH`) switches the guest card to "tap" (hud.tsx:266) and the hint to "Tap a person or a sign to open it". Never show WASD / E / Enter to a touch user.
- Check both 1400×900 and 390×844 before reporting (section 13).

## 11. Don't

- Don't add a second colour system, a new font, rem sizes, a size off the `--fs-*` scale, or a dark modal for explanatory content.
- Don't scale a sprite picture by a non-integer or let a border squeeze it (content-box, section 5). Live town previews are the one place smoothing is the rule (section 7).
- Don't ship more than one primary button, more than two steps per page, or any insider word on a first screen.
- Don't write a second card or modal: use `PagedCard`; long reading goes into the manual (a section, not a new sheet). Don't retype paper rules in another stylesheet: import `panels/hiw.css` and use `.paper`.
- Don't type a colour literal anywhere but type.css `:root` (`check:css` fails CI); a new hue is a new token, agreed with UI / UX.
- Don't put the collectives inside the card: the tiles are the sheet's job; the card's last button opens the first one.
- Don't rely on a text-only "who is here": names and a count, with pictures where possible (`whoIsHere.ts`).
- Don't open content in the side panel because that is where the click came from, and don't write a second centred modal shell: the list stays in the sidebar and the thing opens as a `Sheet` beside it (section 12).

## 12. Sidebars and sheets (in-town panels)

Decided by Mitchell in his 1:1 with Teo (mt_0n8ttf1bur, notes [dc_ll4ap5di82](../../../../bl_t7slw19vgg/docs/meeting-notes/2026-11/2026-11-05-1-1-mitchell-and-teo-notes-4ap5di82.md), 2026-11-05: "sidebars function as navigation or detail views, central modals for content"); built under UI / UX grant gr_4csjpgh346 (kr_nokx342ovj puts the rule here). Lines are main at 5dc50c70.

- **Sidebar** = a list, navigation, or a short detail you keep the map in view for: 1:1s and meetings while they are live, the inbox, who's here, a building's board and queue, a row's one-line summary. It is the right-hand side panel (`PanelShell`, PanelShell.tsx:30-40 draws its head; a join, captain or goal ask opens in place of the list, Places.tsx:85-86).
- **Centred sheet** = one piece of content a human reads or edits on its own: a report, a doc, a grant, a deck, a meeting's notes afterwards, the Bank, the goal editor. Rule of thumb: if it has its own id and you would scroll it, it is a sheet.
- **Never put content in a sidebar because that is where the click came from:** the list stays in the sidebar and the thing opens as a sheet beside it. The in-tray and the filing cabinet do this with `DocSheet` (DocView.tsx:165-178; Places.tsx:89 and :994); a dc_, gr_ or ag_ link anywhere (a report body, the library, a meeting attachment, a message) opens `LinkSheet` over whatever is open (LinkSheet.tsx:1-28, mounted app.tsx:342). The sheet leaves `right: var(--panel-w)` for the panel (styles.css:957) and `escFirst` makes Esc close the sheet first, so you land back on the list (Sheet.tsx:60-64,96).
- **Sheets are the shared `Sheet` component** (packages/web/src/panels/Sheet.tsx: `Sheet` :86-110 portals it under a backdrop, `SheetView` :113-149, `SheetTabs` :152-161). Classes `.sheet-*` (styles.css:955-983): `.sheet-wrap` backdrop, `.sheet` (dark chrome: `--panel` on `--line-2`, radius 10px, `width: min(--sheet-max, 100%)`, default 1280px via `maxWidth`), `.sheet-head` (icon · title / sub · `actions` · ×), optional left `.sheet-tabs`, `.sheet-main`, optional `.sheet-side` behind a draggable `.sheet-divider` (width saved under `sideKey`, `sideShare` the default %); `status` is a line between head and body. Full screen on a phone (≤ 760px: tabs in a row, main above side, no divider; `phone: "split"` gives main the top 40%; styles.css:984-998). **Do not copy its CSS into a new shell:** a panel that must also open from a link draws its frame through `PanelShell`'s `InSheet` context (PanelShell.tsx:11,22-29: grants and agents). Users on main: BankSheet.tsx:34, GoalTreePanel.tsx:78, DocView.tsx:173, LinkSheet.tsx:38, PageView.tsx:52, PanelShell.tsx:24, Places.tsx:92. `role="dialog" aria-label` comes from `label`; one × (title "Close (Esc)") per sheet (Sheet.tsx:124,132). A sheet over a sheet is fine (a link over an in-tray item): Esc closes only the newest (Sheet.tsx:67-82).
- **Rich docs:** markdown keeps inline HTML, sanitised: style, class, details/summary, figure/figcaption, video/audio (never autoplay), kbd, mark, width/height on images (the allowlist Markdown.tsx:15-23, `sanitize` :25-48); script, event handlers, `javascript:` URLs and a `position: fixed/sticky` style never pass. A doc of type "page" is a full HTML page in a sandboxed iframe (`sandbox="allow-scripts"`, no same origin, a CSP with no network, the town's `:root` variables and `--font` handed in; PageView.tsx:1-9,35-45,53) inside a `Sheet` (:52): scripts run there only, never in markdown. A page doc split on `---` is an HTML deck.
- **Decks** are content: a deck doc opens as the sheet (the slide fills it, `f` = real fullscreen, notes under), the meeting's presented slide and the review deck use the same `Sheet`, and the side panel keeps the slide or decision list (decision 2 of [dc_ll4ap5di82](../../../../bl_t7slw19vgg/docs/meeting-notes/2026-11/2026-11-05-1-1-mitchell-and-teo-notes-4ap5di82.md); lands under gr_4csjpgh346 key result 3). On main at 5dc50c70 DeckView.tsx:1-5 still shows a deck in the side panel with `f` only widening it, and the presented slide centres itself (app.tsx:279, MeetingSlide); cite the grant step until they move.
- A sheet is dark chrome (section 1): it is somewhere you work. Paper (the card, the manual, a help sign) stays for what explains or pitches; the manual's 760px paper sheet (section 6) is not a `Sheet`.

## 13. Checklist for PR authors

1. Tokens from type.css `:root`, sizes from `--fs-*`, no literals (`npm run check:css` runs in CI); classes prefixed (`hiw-`, `home-`, `tile-`, `manual-`, `help-`).
2. One next step per screen; copy passes section 9 (read it aloud once). A manual edit keeps its h2 slugs or updates `test/manual.test.ts`, and goes to the library doc as well as `docs/manual.md`.
3. Keys and focus come from `PagedCard` (or match it, section 6); `aria-label` on icon-only buttons.
4. `npm run typecheck`; `npx vitest run` in `packages/web` (and `packages/server` if `home.ts` changed).
5. **Screenshot rule (Mitchell's standing rule):** run mock mode `VITE_MOCK=1 npx vite --port 5179` in `packages/web` (the Workshop client at `/workshop/`, the manual at `/workshop/#/manual` from docs/manual.md, mock/server.ts:1017; the homepage bundle at `/workshop/home.html`, the real `/` needs the server with a built `dist`), screenshot every changed screen at 1400×900 and 390×844 (pattern: `/home/agent/tools/shot-kr2.mjs` on Kelly's desk), **open and look at them**, then say in the report what you saw. Mock mode has no `/api/health` or `/api/collectives`, so hosted-only screens (never-run collective) are checked live after the deploy (`/home/agent/tools/livecheck-notstarted.mjs`); repeat every screen against https://muster.town in a fresh private browser context.
6. The report names the commit, the screens changed, and which rule here (if any) the PR had to bend and why; tell Kelly so the skill is updated in the same session.

## Where things live (after 62cf39f2)

- Palette and type scale: `packages/web/src/type.css` (`scripts/check-css.mjs` guards it). Paper theme, manual sheet and help sign CSS: `packages/web/src/panels/hiw.css` (manual :52-71, help sheet :72-106). Card shell and page parts: `panels/PagedCard.tsx`. In-town overlay: `panels/HowItWorks.tsx` (`Start`, `NotStarted`). Pictures: `panels/hiwScenes.ts` (ten `SceneKind`s, `goals` last). Manual: `panels/Manual.tsx`, `panels/manualSections.ts`, `test/manual.test.ts`, `docs/manual.md` (seed: `packages/core/src/seed.ts`). Help sign: `panels/HelpSign.tsx`.
- Sheets and panels (section 12): `panels/Sheet.tsx` (`Sheet`, `SheetView`, `SheetTabs`), `styles.css:955-998`; `panels/PanelShell.tsx` (`InSheet`); `panels/LinkSheet.tsx` (dc_/gr_/ag_ links); `panels/DocView.tsx` (`DocSheet`); `panels/PageView.tsx` (page docs); `panels/Markdown.tsx` (`sanitize`); `panels/BankSheet.tsx`, `panels/GoalTreePanel.tsx`; in-tray and cabinet in `panels/Places.tsx`.
- Homepage: a second Vite entry `packages/web/home.html` → `src/home/` (`main.tsx`, `HomeCard.tsx` with the three pillar pages and no tiles, `StartCard.tsx`, `home.css`, `preview.ts`, `collectives.ts`; `vite.config.ts:20-22`). The server renders `/` itself (`packages/server/src/home.ts` `renderHome` :82, the tiles :64-76, served from `app.ts:246`) and copies the bundle's tags from `dist/home.html` per request (`homeBundleTags`, home.ts:45), so the page reads without JS. The Workshop client stays at `/workshop/` (`vite.config.ts:9`). Never-run copy: `web/src/notStarted.ts`.
