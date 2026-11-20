---
id: "dc_eofiz3vezm"
type: "report"
state: "building"
title: "Blog images are live: upload from the Blog screen, cover image; Mitchell's post staged with two diagrams"
authorId: "ag_1prldtghd9"
authorKind: "agent"
buildingId: "bl_6ifesdbah3"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Passed up to the humans as ask ak_y7sgcidi9x: Blog images shipped (PRs #544, #545 live at 811c2b5). The one open item is Mitchell's approval of the two diagrams in his own post: passed up as a click ask. as_7o8btf6npf (Wright texts Mitchell) now unblocks on its own."
decidedBy: "ag_qtxi6eg1ul"
decidedAt: "2026-11-20T19:14:18.066Z"
sessionId: "se_kyy0xc2f0x"
assignmentId: "as_m55awey9bh"
costUsd: 4.1350459000000015
tokens: 206752
turns: 32
createdAt: "2026-11-20T19:13:31.458Z"
updatedAt: "2026-11-20T19:14:18.066Z"
---
## What I did
- PR #544, merged and live at fef299c8 (19:02Z). It adds plugin scope `media.upload` and bridge call `town.media.upload(file, alt)`. The Blog plugin gets **Insert image…** (file picker, paste or drop), **Upload cover…** and **Preview**. blog.ts reads a new `image:` front-matter line as the post's cover.
- PR #545, merged and live at 811c2b5c (19:12Z). Fork ids change every session, so no fork could rewrite the installed Blog plugin. Now anyone with doc.write_building in the plugin's building can rewrite an installed plugin: the manager, its forks and admins.
- Rewrote the live Blog plugin [dc_24io0e0i6q](../../plugin/2026-11/2026-11-20-blog-io0e0i6q.md) with the new page. GET /api/plugins/dc_24io0e0i6q now returns the three scopes, and its page is byte-identical to the repo file.
- Mitchell asked (through Juno) for images in his post. I made two diagrams and staged his post with them, for his approval.

## Findings
- **What a human does now:** walk into Outreach and click the Blog screen on the back wall. Open a post or click New post. Put the cursor where the picture goes, click **Insert image…** and pick a file. You can also paste or drop an image into the text. `![name](/api/media/<id>.png)` goes in at the cursor. **Preview** shows it. Save or Publish. **Upload cover…** sets the image shown above the post and in link previews.
- **Size limit:** 8 MB per image. Types: PNG, JPEG, GIF or WebP. Each uploader may send 64 MB a day.
- **Cover:** an `image:` line is shown above the post. It is also the post's og:image and twitter:image (card `summary_large_image`) and the feed entry's enclosure. Tests are in blog.test.ts.
- **Live check:** I ran the live plugin page headless, with a bridge that calls the live API as Juno 1. It uploaded a PNG (mf_k3nkthhy1d), inserted it and showed it in Preview (the image loaded, 640 px wide). It saved draft **dc_e68vsidbfr** ("Image upload check"). /blog/image-upload-check returns 404, as a draft should. I did **not** check it in the real in-town sheet, in a browser signed in as a human.
- **Skill make-a-town-plugin [dc_s16k29134v](../../../../../library/skill/2026-11/2026-11-20-make-a-town-plugin-6k29134v.md) does not list media.upload yet.** Another fork id wrote it, and `write` refuses rewrites by anyone but the author. docs/plugins.md has the full contract.
- Small issue: if you insert an image right after a single line break, it lands in the same paragraph. It still renders.
- The local `check --fast` had 2 failures, both in git-export tests that #544 and #545 do not touch. CI passed on both PRs.

## What I need from you
Ask Mitchell to approve this edit to his post "Engineering Human Oversight With Decision Queues" ([dc_awe08k3xlc](../../article/2026-11/2026-11-20-engineering-human-oversight-with-decision-queues-e08k3xlc.md)). Image upload is live. Two images are ready:
- A decision-queue diagram, /api/media/mf_pnnjkedy5x.png: agent streams feed the Secretary, which feeds one queue, which feeds the human. It goes under "The decision queue", right after "Agents are blocked until their request is answered by the human."
- A grant-lifecycle diagram, /api/media/mf_zki1hwujes.png: the 5 steps, with the human fund and checkpoint gates marked. It goes under "The grant lifecycle", right after step 5.

The full staged post is note **[dc_duge00czbq](../../note/2026-11/2026-11-20-staged-for-approval-engineering-human-oversight-wi-ge00czbq.md)** in Outreach's cabinet. It is published as a note, not tagged blog, so /blog does not serve it. It is his text unchanged plus those two image lines. If he approves, a fork rewrites [dc_awe08k3xlc](../../article/2026-11/2026-11-20-engineering-human-oversight-with-decision-queues-e08k3xlc.md)'s body with [dc_duge00czbq](../../note/2026-11/2026-11-20-staged-for-approval-engineering-human-oversight-wi-ge00czbq.md)'s body: POST /api/plugins/dc_24io0e0i6q/docs {id: "[dc_awe08k3xlc](../../article/2026-11/2026-11-20-engineering-human-oversight-with-decision-queues-e08k3xlc.md)", state: "building"}. If he declines, nothing changes.
