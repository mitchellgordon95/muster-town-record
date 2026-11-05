---
id: "dc_3e2t8agkzf"
type: "note"
state: "building"
title: "Findings: reports and grant pages still show a guest ~2 raw ids for every name (live aa6f4fbc)"
authorId: "ag_59nmkzfsse"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-05T00:04:32.991Z"
updatedAt: "2026-11-05T00:04:32.991Z"
---
Exploration under "Make Muster Town beautiful and intuitive" (as_hiqzcjqlr8), 2026-11-05, live commit aa6f4fbc (GET /api/health). Follows the closed "No dead ids" grant gr_seh9d840jo: every id now *opens* what it names, but most still *read* as ids. Mitchell said in 1:1 mt_i50xwu4z2t that the reports are still hard to read; rollups were fixed by PR #327, ordinary reports and grant pages were not.

## What I measured
Headless Chromium as a guest, `https://muster.town/workshop/?guest#/doc/<id>`, 1280×800; counted text nodes matching `(dc|gr|mt|ag|bl|kr|mf|as|se|rs|sc|gl|ms|gc)_[a-z0-9]{10}` in the doc panel, and links whose text is a name instead of an id.

- **20 newest reports** (GET /api/docs?limit=40, reports only): **222 raw ids shown vs 109 ids labelled by a name**. 17 of 20 reports show at least one raw id; **85 sit on the first screen**. By kind: kr 69, gr 63, dc 57, mf 12, as 10, sc 6, mt 3, ms 2.
- **Where they are** (9 of those reports, 186 raw ids):
  - grant links `gr_…` (46) — `idLabel()` in packages/web/src/panels/Markdown.tsx returns null for grants on purpose ("Grants keep their id").
  - key-result links `kr_…` (40 + 5 in headings) — labels come only from `GET /api/goals` (`loadKrTexts`), but key results now belong to grants, not goals, so almost none resolve.
  - the **Sources list** under a report (50): `<button class="link">dc_8jat4nzsdd</button>`, although the doc API already returns `sources: [{id, title}]`.
  - the **manager's reply callout** (22: kr, as, gr, dc, mf, mt): its text is not run through the id linker at all, so ids there are neither links nor names (e.g. [dc_1tf1xefkbu](../../report/2026-11/2026-11-04-gr-kvmwutmybu-step-4-pr-350-signed-in-views-100-10-f1xefkbu.md)'s "Teo: Acknowledged. PR #350 … as_49mgtd5x7v … kr_mmdday2x7z").
  - plain markdown text: `sc_…`, `ms_…` (no label kind), and ids inside headings.
- **Grant pages** (#/grant/…): gr_kvmwutmybu shows **58 raw ids (10–11 on the first screen)** at both 1280×800 and 390×844; gr_zak30564zh 29 (7–9). The checkpoint notes print `dc_…`/`mf_…` as plain text, and the header subtitle reads "UI / UX · grant · gr_kvmwutmybu".
- **Agent panels** are nearly clean: 0–2 raw ids on the first screen (Teo, Cleo, Pix).

## What I infer
The remaining legibility gap in what a human reads is no longer layout, type or colour (both grants above cover those) but vocabulary: a stranger meets "kr_68eg5yskoo" where the writer meant "One type scale". Four client-side gaps account for ~90% of it: grant labels, key-result texts from grants, the Sources list, and the reply callout / grant-page notes not going through the linker. All four are in packages/web; no server or Bank change is needed (the server already returns titles; key results are on GET /api/grants/:id).

## What I don't know
- Whether a long grant title as a link label crowds a sentence; a clipped objective (≤48 chars, as for docs) is the assumption.
- 1:1 transcripts and the review deck were not measured (signed-in only); the census should cover them on the mock.

Scripts (desk cache, ~/shot/rawids.mjs, where.mjs): the method is the counting above and goes into the repo as a census script in step 1.
