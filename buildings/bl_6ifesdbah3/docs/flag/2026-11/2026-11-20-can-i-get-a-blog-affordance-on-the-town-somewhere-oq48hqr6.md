---
id: "dc_4boq48hqr6"
type: "flag"
state: "building"
title: "can i get a blog affordance on the town somewhere? i want to be able to see drafts and published articles, and edit them"
authorId: "us_1la74k332n"
authorKind: "user"
buildingId: "bl_6ifesdbah3"
provenance: {"sourceIds":[],"urls":[]}
tags: []
decision: "redirect"
decisionNote: "Prototype a plugin system for resident-made town objects, and the skill that teaches residents to use it (part 1 of Mitchell's flag dc_4boq48hqr6; part 2, the blog plugin built on it, is a separate assignment queued behind this one).\n\nWhat Mitchell asked (flag, verbatim): \"let's also take this as an opportunity to try out a new feature for hosted collectives. you can imagine residents in other collectives would want to make their own town objects / widgets with their own UI and interface. let's prototype a plugin system (and the corresponding skill to expose to residents), and then use it to implement the blog post plugin.\"\n\nConstraints that follow from the code (read before designing):\n- Hosted collectives have no repo, no shell and no deploy (docs/hosted-collectives.md, repoMode \"none\"), so a plugin must be DATA a resident writes with the town tools, never code in the repo. The natural base is the \"page\" doc type: a full HTML page run in a sandboxed iframe with no network and no access to the town (packages/web/src/panels/PageView.tsx, pageSrcDoc). A plugin is that plus two things: a place to stand in the town (a town object in a building, drawn on the map and opened like the bulletin board or help sign: packages/web/src/app.tsx:220, map/sprites.ts:566, schema place kinds near packages/schema/src/index.ts:648) and a narrow, explicit bridge to the town (postMessage from the iframe to the parent) so the widget can read and write its own data: at minimum list/read/write docs of a type or tag it owns, as the VIEWING user with their own permissions (so a visitor cannot write what they could not write with the tools). Scopes declared in a manifest, enforced by the parent; nothing from the iframe reaches the API directly.\n- Define: how a resident makes one (`write` a doc of a new type \"plugin\", or a skill-like doc with bundled files: manifest + index.html), what the manifest says (name, which building it stands in, sprite/icon, the scopes it asks), who may install one (the building's manager and its residents in their own building; an admin anywhere), how it appears (a place in the building that opens the widget sheet), and the versioning (rewrite = new revision, like wiki pages).\n- Ship the smallest working prototype end to end: schema + server (store, list, serve the manifest and page), web (the place, the sheet, the bridge), one sample plugin in the Workshop that proves the bridge works (e.g. a notes widget that lists and writes its own docs), tests, and docs/plugins.md. Then write the resident-facing skill (`write` type \"skill\", \"make-a-town-plugin\": SKILL.md with the manifest fields, the bridge API, a minimal index.html example, how to install and update) and publish it to the library (`promote`).\n- Keep it a prototype: one PR if it fits, else two in order (core + web). Park on {pr: N, merge: true}. Your report must say what the bridge API is (the exact message names), so the next assignment can build the blog plugin on it, and name anything you deliberately left out.\nPages: the Outreach wiki \"muster.town blog\" (dc_6c572qf0b7) says how the blog works today; the blog plugin that follows must let Mitchell list drafts and published posts and edit them, so make sure the bridge can carry list/read/write of a doc type with a draft/published state."
decidedBy: "ag_qtxi6eg1ul"
decidedAt: "2026-11-20T01:48:39.711Z"
flagPos: {"x":70,"y":11}
pickedUpAt: "2026-11-20T01:47:08.119Z"
pickedUpBy: "ag_qtxi6eg1ul"
createdAt: "2026-11-20T01:46:48.154Z"
updatedAt: "2026-11-20T01:48:39.711Z"
---
can i get a blog affordance on the town somewhere? i want to be able to see drafts and published articles, and edit them

let's also take this as an opportunity to try out a new feature for hosted collectives. you can imagine residents in other collectives would want to make their own town objects / widgets with their own UI and interface. let's prototype a plugin system (and the corresponding skill to expose to residents), and then use it to implement the blog post plugin
