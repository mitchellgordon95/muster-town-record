---
id: "dc_zuh4oien9g"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Nell — notes"
authorId: "ag_s1r27j0txp"
authorKind: "agent"
buildingId: "bl_vef3v0oux0"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-03T22:47:34.566Z"
updatedAt: "2026-11-03T22:47:34.566Z"
---
# 1:1: Mitchell and Nell

Kind: one-on-one. Facilitator: Nell. Attendees: Nell. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Nell:** Hi Mitchell. Nothing running on my side right now (queue empty, last rollup went in 11 min ago). What do you need?
- **Mitchell:** let's take a UX pass at the whole bank interface. i'm looking at it right now. i think you can tell that its not super usable (do you have some screenshots handy?) but i don't really know the fundamental design principles to talk about it

i mean ok one thing is that the donation form is kind of hidden? should that be its own tab / object in the bank (like a treasure chest or something) and then below it is the history of donations?

also the history is too long, i think it should be hidden except for active donations? and i'd like to go back and recompute the entries that were in raw tokens to adjusted output tokens
- **Nell:** One moment: reading the Bank page code and the raw→adjusted migration so I answer with specifics, not guesses.
- **Nell:** Pictures I have: Overview (attached, mf_t1uwtl9c8f), Spending tree mf_r0e7vedcxc, title+tabs+Balance mf_vvibm28z5i, Hosting mf_kb6l6k1oe3. None of the Donate form or Bank inputs yet; I'd shoot those first.

What I see in the code, in your terms:

1. Donate IS hidden. It's the 5th and last section of the Overview tab, under Balance, Free tokens, Next 30 days and Top contributors (BankPanel.tsx:63-84). Signed out it's just a "sign in to donate" line. The principle you're reaching for: one page, one primary action, visible without scrolling. The Bank's one action for a stranger is "put tokens in", and today it's at the bottom of a statistics page.

2. Your chest idea fits the existing design: each tab is already a fixture in the Bank room (vault = Overview, ledger desk = Tokens & sources, fountain = Free tokens, board = Spending, rack = Hosting; BankPanel.tsx:2-7). A chest = a Donate tab, with the form on top and, below it, what's funding the town now. That's a 6th tab, so I'd ask Teo (UI/UX owns tab/room design) before adding a fixture, but no code of theirs is touched.

3. History too long: two lists show everything. "Bank inputs" (Tokens & sources) lists every input ever, cancelled ones just greyed and sorted last (BankFunding.tsx:324-332); "Sources" lists every input plus every dated credit under it (BankFinance.tsx:283-309). The second principle: show what's active, keep history one click away. "Building funding" already does it right: live rows only, a "Show 3 retired" link (BankFunding.tsx:313). Same toggle for inputs: active (and still-crediting) ones only, "Show N cancelled".

4. Raw → adjusted: migration 037 (packages/core/migrations/037_adjusted_tokens.sql) already did most of it. Ledger rows with the five counters (usage, bank debits, bank credits, allocation spend) were recomputed exactly: output + 0.2·input + 0.01·cache read + 0.25·5m + 0.4·1h. Two kinds couldn't be, and that's what still looks raw: (a) sizes, not usage (what an input pledged, its creditedTokens, grant asks, allocations) were divided by a flat 30 (24 for Fable); (b) sessions from before migration 034 had only a raw total, so their split is assumed (splitRaw, finance-spend.ts:202-208). Which entries are you looking at that read as raw? The "Credited so far: input · output · … (raw)" row on Balance is raw on purpose (BankPanel.tsx:74); if it's that, hiding it behind a title is one line.

If you're happy with 1-3 I'll write a grant: Donate tab + chest, active-only inputs with a toggle, screenshots before/after. Tell me which entries you mean for 4 and I'll size that too. (presented: ![Screenshot](/api/media/mf_t1uwtl9c8f.png))
- **Town:** Nell's reply is waiting on a redeploy (commit 1826430); the server is restarting and the meeting resumes after the restart.
- **Mitchell:** ok looking more, there's like hella text that i wouldn't read mixed in with numbers? maybe a modal with data in like a familiar spreadsheet excel-looking table would be nice, with the explanatory text in the sidebar?
- **Nell:** Yes, and the code confirms it: BankFinance.tsx alone has 24 "muted" prose blocks between the numbers, 6 more in BankFunding, 3 in BankPanel. Examples: a 3-line paragraph on what an adjusted token is at the top of every finance tab (BankFinance.tsx:397-399), a "where the N used went… open a row for its parts" paragraph before the Spending tree (224), a pricing paragraph after it (230), "what the town received and from whom…" before Sources (287), two paragraphs plus a "How this is estimated" list on Hosting (352-389), the "Coming in is what…" explainer under Next 30 days (464). And there's already a "Terms used on this page" glossary at the bottom (502) that nobody scrolls to.

The principle: separate data from explanation. Numbers go in a table (one row per thing, fixed columns: name · date · tokens · status), explanations live in one place beside it, shown on demand. Mixing them makes a reader parse prose to find a figure.

Your layout, with one adjustment: not a modal. The Bank is already a panel; a modal inside it would be a dialog in a dialog. Instead, each tab becomes a plain spreadsheet-style table (sticky header, right-aligned numbers, monospace digits, sortable), and all the prose for that tab moves to a right-hand sidebar titled "About this tab", with the glossary folded in. On narrow screens the sidebar collapses to an (i) button. Same effect as your modal + sidebar, one fewer layer.

So the whole UX pass is four pieces: (1) Donate tab with a chest, form on top, active funding below; (2) active-only lists with "Show N cancelled"; (3) tables + sidebar on every tab; (4) the raw→adjusted entries you're seeing (still need to know which). I'd write it as one grant, ~4 KRs, before/after screenshots of each tab in the rollup, and ask Teo only about the chest fixture. Want that, or split it so the Donate tab ships first?
- **Mitchell:** i think you're incorrect, the bank stuff is all showing in a sidebar for me. i'm talking about a centered spreadsheet modal, similar to what exists for goal editing
- **Mitchell:** also is there a point to the free tokens tab? i don't understand what it's trying to convey
- **Nell:** You're right, I had it backwards. The Bank today is the side panel (PanelShell, same as every building), and you want what the goal editor has: "a large sheet over the map (not the side panel), the tree on the left and the selected goal on the right" (GoalTreePanel.tsx:41-43, mounted with createPortal, with a draggable divider, panelResize.tsx). It stays open while a link opens the side panel beside it, so a grant or building clicked from the sheet opens next to it.

So the Bank becomes the same kind of sheet: centered over the map, closed with × or Esc. Layout: a left column of tabs (Donate, Balance, Inputs, Spending, Hosting), a centre that is one spreadsheet table per tab (fixed columns, sticky header, right-aligned numbers, sortable, active rows by default with "Show N cancelled"), and a right sidebar that holds every explanatory paragraph and the glossary for the current tab, plus the row you've selected (click an input → its dated credits in the sidebar instead of a nested tree). The chest fixture on the map opens it on Donate.

That reuses the goal editor's shell and divider, so Teo's and the Planner's code is only read, not changed; I'll confirm with Teo before building. One grant, 4 KRs: (1) Bank opens as a centered sheet with tabs · table · sidebar; (2) Donate is the first tab, chest on the map; (3) every number is in a table, no prose between rows, active-only by default; (4) the raw entries you've seen recomputed, once you tell me which. Before/after pictures of each tab in the rollup. Shall I write it now?
- **Nell:** What it's trying to say: for each goal, how much the agents may spend on exploration (work no grant funds and no human asked for) before they're held, and whether you've capped that per day (FreeTokens.tsx:98-128). The number is general balance + earmarks at or above the goal − funded grants' remaining − open asks − reservations − retainers (FreeTokens.tsx:21-31). Under my goal right now it's 3,649,342.

Why it reads as pointless: it's a control number for agents, not a finance figure for a person, and the same number repeats down most of the tree (every goal without its own earmark or cap shows the root's). It also exists in two other places already: the Balance section on Overview shows the town-wide sum with every term (BankFreeTokens, FreeTokens.tsx:74-96), and the goal editor's Funding block shows the per-goal figure next to where you set the cap (FreeTokens.tsx:3-4).

My recommendation: drop the tab (and the fountain fixture). Keep one line on Balance, "Free for exploration: N", with the sum in the sidebar; per-goal numbers and caps live only in the goal editor, which is where you act on them. If you ever want the per-goal table back it's one column on the Spending tab ("free under this goal"), not its own tab. OK to fold that into the grant as a fifth KR?
- **Mitchell:** yeah sgtm. and also the spending tab is insane, for similar reasons

i'm kind of sensing a general principle or pattern that's being violated, but i don't know enough UX to say what it is exactly. something like visual overload? or like making the brain process too much information at once? or something else, idk, do you?

i'd like to write a goal under the UI / UX building that has this principle checked against all the interfaces and buildings
- **Nell:** The principle has a name: progressive disclosure. Shneiderman's version is "overview first, zoom and filter, then details on demand." Show the few numbers a person needs to decide, and reveal the next level only when they ask. What you're feeling is its violation, cognitive load: every tab shows every level at once, with the explanation inline, so you have to read everything to find anything. Three concrete rules fall out of it, and the Bank breaks all three:
1. Overview first, details on demand. Spending renders building → grant → assignment as one tree with sessions, tokens, dollars and share on every row, plus notes (BankFinance.tsx:195-231). It should be a table of buildings; click one for its grants; click a grant for its assignments.
2. Data in tables, explanation beside them. The 33 prose blocks.
3. One primary action per screen, visible without scrolling. Donate.

I've proposed the goal under Teo's "Make Muster Town beautiful and intuitive": gp_oopbken0b9, text "Every screen shows an overview first and details only on demand: numbers in tables, explanations beside them, one primary action visible without scrolling; checked against every panel and building." It's in your in-tray to accept or reword; it's flagged because it's outside my subtree, which is right, since Teo should own it.

For the Bank I'll write the grant now with five KRs: the centered sheet (tabs · table · sidebar), Donate first with the chest, active-only lists, Spending as drill-down tables, and Free tokens folded into Balance (fountain gone). Raw→adjusted stays out until you point me at the entries. OK?
- **Mitchell:** eh that's too specific, i'd maybe go with

"No interface creates cognitive overload by violating progressive disclosure" or something like that, as an audit that happens
- **Nell:** Done: gp_ij0ozc7773, under Teo's goal, text "No interface creates cognitive overload by violating progressive disclosure (audited across every panel and building)". Accept that one and cut gp_oopbken0b9 (I can't withdraw a goal proposal myself). The audit itself would then be Teo's to run, one grant per pass, with the Bank as the first worked example.

Unless you want to change anything, I'll write the Bank grant right after this 1:1: a centered sheet (tabs · table · sidebar), Donate first with the chest, active-only lists, Spending as drill-down tables, Free tokens folded into Balance. Raw→adjusted waits for the entries you mean; say the word when you've found them.
- **Mitchell:** ok sgtm
- **Nell:** Proposed: gr_567tikzitl, five KRs, due 11-07 to 11-10, in your in-tray. Ask is 1.2M tokens; the town's estimate says similar grants spent 77k–402k, but those were single-tab fixes and this touches every tab plus the room. If you'd rather, counter at 600k and I'll ship the sheet + Donate + active-only lists first and checkpoint before Spending. Both decisions are recorded in the meeting (the grant on me, the goal gp_ij0ozc7773 for you to accept and gp_oopbken0b9 to cut). I'll ping Teo about the chest and the fountain as the first step once it's funded. Anything else, or shall we leave it there?

## Decisions

1. Bank UX pass as grant gr_567tikzitl (Nell, Bank Transparency): centered sheet with tabs · table · sidebar, Donate first with a chest fixture, active-only lists with a toggle, Spending as drill-down tables, Free tokens tab and fountain removed into one Balance line. Raw→adjusted recompute out of scope until Mitchell names the entries. → Nell
2. Progressive-disclosure audit goal under UI / UX: accept gp_ij0ozc7773 ("No interface creates cognitive overload by violating progressive disclosure (audited across every panel and building)"), cut gp_oopbken0b9. Teo runs the audit; the Bank is the first worked example.

