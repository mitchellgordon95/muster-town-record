---
id: "mt_x3qozh4j7m"
kind: "one-on-one"
buildingId: "bl_6ifesdbah3"
title: "1:1: Mitchell and Juno"
scheduledAt: "2026-11-20T18:36:42.672Z"
phase: "done"
facilitatorId: "ag_qtxi6eg1ul"
attendeeIds: ["ag_qtxi6eg1ul"]
agenda: ""
brings: {"mode":"status","text":""}
askHumans: false
deck: null
summaries: {}
transcript: [{"speakerId":"ag_qtxi6eg1ul","speakerKind":"agent","text":"Hi Mitchell. Juno here, Outreach. What do you need?","at":"2026-11-20T18:36:51.220Z"},{"speakerId":"us_1la74k332n","speakerKind":"user","text":"good work on the plugins! can i also get image support in  blogs","at":"2026-11-20T18:37:11.391Z"},{"speakerId":"ag_qtxi6eg1ul","speakerKind":"agent","text":"Thanks. Yes. Half of it already works: a post body with `![alt](/api/media/<id>.png)` renders as an image on /blog, and the town has an upload endpoint for png, jpeg, gif and webp. What's missing is the editor side: the Blog plugin can only read and write docs, so there's no upload button. I've just queued it as directed work from this 1:1: a media upload scope for plugins, an \"Insert image\" button in the Blog editor that uploads and drops the markdown in at the cursor, and an optional cover image per post used for the og:image and the feed. One PR, merges when green. Want anything else in it, like drag-and-drop or image resizing?","at":"2026-11-20T18:38:06.892Z","tools":[{"what":"Reading \"muster.town blog\"","result":"{\"id\":\"dc_6c572qf0b7\",\"type\":\"wiki\",\"state\":\"building\",\"title\":\"muster.town blog\",\"body\":\"# muster.town blog (as of 2026-11-20 02:38 UTC, server clock)\\n\\nBuil…"},{"what":"Grepping for api/media"},{"what":"Grepping for img|image|!\\["},{"what":"Grepping for router\\.(get|post)\\(|maxSize|MAX_|mimetype|conten…"},{"what":"Grepping for scopes?\\b.*(media|upload)|\"media\"|'media'"},{"what":"Grepping for SCOPES|scopes =|allowedScopes"},{"what":"Queuing work: Image support in the blog: upload from the Blog plugin edit…","result":"{\"assignmentId\":\"as_m55awey9bh\",\"lane\":\"directed\",\"pages\":[\"dc_6c572qf0b7\",\"dc_8an7b5hviv\"],\"queue\":\"building\"}"}]}]
decisions: [{"text":"Image support in the blog: a media upload scope for plugins, an Insert image button in the Blog plugin editor that uploads and inserts the markdown, and an optional cover image per post for og:image and the feed. Queued on the Outreach building queue as as_m55awey9bh (directed, source this 1:1).","assigneeId":"ag_qtxi6eg1ul","assignmentId":"as_m55awey9bh","queueBuildingId":"bl_6ifesdbah3","lane":"directed","sourceId":"mt_x3qozh4j7m"}]
notesDocId: "dc_6uk7zx907x"
withUserId: "us_1la74k332n"
createdAt: "2026-11-20T18:36:42.672Z"
startedAt: "2026-11-20T18:36:42.672Z"
endedAt: "2026-11-20T18:41:20.816Z"
---
# 1:1: Mitchell and Juno

- **Juno** (2026-11-20T18:36:51.220Z): Hi Mitchell. Juno here, Outreach. What do you need?
- **Mitchell** (2026-11-20T18:37:11.391Z): good work on the plugins! can i also get image support in  blogs
- **Juno** (2026-11-20T18:38:06.892Z): Thanks. Yes. Half of it already works: a post body with `![alt](/api/media/<id>.png)` renders as an image on /blog, and the town has an upload endpoint for png, jpeg, gif and webp. What's missing is the editor side: the Blog plugin can only read and write docs, so there's no upload button. I've just queued it as directed work from this 1:1: a media upload scope for plugins, an "Insert image" button in the Blog editor that uploads and drops the markdown in at the cursor, and an optional cover image per post used for the og:image and the feed. One PR, merges when green. Want anything else in it, like drag-and-drop or image resizing?
