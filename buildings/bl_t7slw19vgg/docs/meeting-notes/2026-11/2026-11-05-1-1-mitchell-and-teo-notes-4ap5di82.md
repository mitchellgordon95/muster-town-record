---
id: "dc_ll4ap5di82"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Teo — notes"
authorId: "ag_s1kuuuo54b"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-05T20:14:49.552Z"
updatedAt: "2026-11-05T20:14:49.552Z"
---
# 1:1: Mitchell and Teo

Kind: one-on-one. Facilitator: Teo. Attendees: Teo. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Teo:** Hi Mitchell — Teo here. What do you need?
- **Mitchell:** i've been thinking about the UIs a little bit. we've been cramming a lot into sidebars. sometimes that's ok, like with 1:1 chats etc.

but there's a bunch of times where we could use the center space for a like focused modal on content

the bank and the goal editor are already good examples of this.

i think we should add this to the style guide or something, but having sidebars function as like navigation or detail views, while having central modals for like, content. not sure how else to describe it

but like one example might be the intray, clicking on reports in the list and seeing the full contents in a main modal. not sure of other places where we can apply a similar UX pattern
- **Teo:** Agree, and the code already half-says it: the goal editor (.ge-*) and the Bank (.bank-*) are the same centred sheet, copy-pasted (styles.css:960 says so outright). The rule as I'd write it: **sidebar = list, navigation, or a short detail you keep the map in view for (chat, who's here, a row's summary); centred sheet = one piece of content you read or edit on its own (a report, a doc, a grant, a meeting's notes, a deck).** Rule of thumb: if it has its own id and you'd scroll it, it's a sheet.

Where I'd apply it, in order of payoff:
1. In-tray: the list stays in the sidebar, clicking a report/proposal opens it as a sheet with the Your-call block, cards and the decide buttons. Same for the building filing cabinet.
2. Any doc opened from a link (dc_ in a message, the library, a meeting attachment): today they land in the sidebar at 380px.
3. Grant cards (gr_ links, the checkpoint card) and agent profiles.
4. Meeting transcript: sidebar is right for live talk, but the notes/deck afterwards are content, so a sheet.
Keep in sidebars: 1:1s and meetings while live, inbox, who's here, the board, the building's queue.

Work I'd queue: (a) one shared Sheet component the Bank and goal editor both use, (b) in-tray report → sheet, (c) docs/grants/agents → sheet, (d) the rule in Kelly's style-guide skill ([dc_q736158pnn](../../../../bl_hzjw0z0zlz/docs/skill/2026-10/2026-10-26-muster-style-guide-36158pnn.md); it's Onboarding's, so I'll send her the wording). Want me to do (a)+(b) first and roll up, or the lot?
- **Mitchell:** put it all under a grant i think

and while we're at it, let's think about how we can display not just like markdown docs, but rich html docs
- **Teo:** One grant it is. On rich HTML, here's what's true today: every doc goes through marked plus an allowlist that keeps ~30 tags and only href/src/alt/title (panels/Markdown.tsx:15-16); class and style are stripped, so an agent writing HTML gets plain markdown-looking output. Two levels I'd put in the grant:

1. **Richer inline HTML in any doc:** allow style/class, details/summary, figure/figcaption, video/audio, kbd, mark, and width/height on images, still sanitised. Cheap; covers tables with colour, callouts, side-by-side images.
2. **A real rich doc:** a doc whose body is a full HTML page (new type "page", or a ```html block that is the whole doc) rendered in a sandboxed iframe in the centred sheet, with the town's CSS variables handed in so it matches the theme. The sandbox keeps it from touching the session token. That gives agents charts, layouts, embedded SVG, a proper report.

The one call for you: do rich docs get to run **scripts**? With `sandbox="allow-scripts"` (no same-origin) a doc can draw an interactive chart but can't read the token or the page. I'd say yes, scripts in the iframe only; markdown docs never. If you're fine with that, I'll propose the grant now: key results = (1) one shared Sheet, Bank and goal editor on it; (2) in-tray report and filing-cabinet doc open as a sheet; (3) docs, grants, agents from links open as a sheet; (4) the rich-HTML levels above with a sample page in the library; (5) the rule in the style guide. Ask around 900k tokens.
- **Mitchell:** sgtm
- **Teo:** Filed: gr_4csjpgh346, 900k, five key results (shared Sheet with Bank + goal editor on it by the 9th; in-tray and filing cabinet open as sheets by the 12th; docs/grants/agents from links by the 14th; rich HTML both levels plus a sample chart page in the library, and the style-guide rule, by the 16th). It's in your in-tray to fund. Scripts: page docs in the sandbox only, never markdown. Once it's funded I'll queue step 1 and send Kelly the style-guide wording. Anything else? (presented: Grant: Sidebars for lists, navigation and live talk; a centred sheet for content: one shared Sheet component, in-tray reports and docs open in it, and rich HTML docs render in it. (page grant:gr_4csjpgh346))
- **Mitchell:** oh also how do slideshows fit into this? i haven't really used the feature in a long time
- **Teo:** Slideshows are the clearest case for the sheet. Three live today: a deck doc shows one slide at a time *in the side panel*, with `f` only widening the panel to its max (DeckView.tsx:2-5); a slide presented in a meeting already centres itself on the map as a modal (app.tsx:268, MeetingSlide); and the review deck is your in-tray as slides. So it's the pattern done three ways. Under the grant: a deck is content, so it opens as the sheet (16:9 slide filling it, `f` = real fullscreen, notes under), the meeting's presented slide and the review deck use the same Sheet, and the side panel keeps the list of slides/decisions. Rich pages fit too: a "page" doc split on `---` is an HTML deck, so a chart can be a slide. That sits inside key result 3 (decks are docs) and I'll note it on the grant; no change to the ask.
- **Mitchell:** ok
- **Teo:** Recorded as decision 2 on the meeting. Nothing more from my side: gr_4csjpgh346 waits in your in-tray, and the moment it's funded I queue the Sheet component and send Kelly the style-guide wording. End the 1:1 whenever you like.

## Decisions

1. Sidebars for lists, navigation and live talk; a centred sheet for content. One grant (gr_4csjpgh346, 900k ask) covers: shared Sheet component (Bank + goal editor on it), in-tray reports and filing-cabinet docs open as a sheet, docs/grants/agents from links open as a sheet, rich HTML (wider sanitizer allowlist + doc type 'page' in a sandboxed iframe with scripts allowed there only), and the rule in the style guide (wording sent to Kelly). Mitchell: 'put it all under a grant', 'sgtm' on scripts in the sandbox.
2. Decks under gr_4csjpgh346 key result 3: a deck doc opens as the centred sheet (slide fills it, f = real fullscreen, notes under); the meeting's presented slide (MeetingSlide) and the review deck use the same Sheet; the side panel keeps the slide/decision list; a page doc split on --- is an HTML deck. No change to the ask. Mitchell: 'ok'.

