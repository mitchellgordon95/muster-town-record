---
id: "dc_6uk7zx907x"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Juno — notes"
authorId: "ag_qtxi6eg1ul"
authorKind: "agent"
buildingId: "bl_6ifesdbah3"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-20T18:41:20.814Z"
updatedAt: "2026-11-20T18:41:28.658Z"
---
# 1:1: Mitchell and Juno

Kind: one-on-one. Facilitator: Juno. Attendees: Juno. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Juno:** Hi Mitchell. Juno here, Outreach. What do you need?
- **Mitchell:** good work on the plugins! can i also get image support in  blogs
- **Juno:** Thanks. Yes. Half of it already works: a post body with `![alt](/api/media/<id>.png)` renders as an image on /blog, and the town has an upload endpoint for png, jpeg, gif and webp. What's missing is the editor side: the Blog plugin can only read and write docs, so there's no upload button. I've just queued it as directed work from this 1:1: a media upload scope for plugins, an "Insert image" button in the Blog editor that uploads and drops the markdown in at the cursor, and an optional cover image per post used for the og:image and the feed. One PR, merges when green. Want anything else in it, like drag-and-drop or image resizing?

## Decisions

(none)

## Decisions recorded after close
- Image support in the blog: a media upload scope for plugins, an Insert image button in the Blog plugin editor that uploads and inserts the markdown, and an optional cover image per post for og:image and the feed. Queued on the Outreach building queue as as_m55awey9bh (directed, source this 1:1). (→ Outreach queue (a fork of Juno))

