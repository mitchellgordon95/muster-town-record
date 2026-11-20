---
id: "dc_umioej89iy"
type: "flag"
state: "building"
title: "i don't understand why the water coming out of the fire hydrant is always pointing at the secretary? just make it do a …"
authorId: "us_1la74k332n"
authorKind: "user"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
decision: "redirect"
decisionNote: "Mitchell's flag (dc_umioej89iy, 2026-11-20 01:37 UTC): \"i don't understand why the water coming out of the fire hydrant is always pointing at the secretary? just make it do a little ark and form a small pool.\"\n\nWhy it points at the Secretary: packages/web/src/map/renderer.ts:600-603 picks `settle` = the Secretary's desk tile (else the hydrant) and passes it as `to` into streamParticles (packages/web/src/map/hydrant.ts:46-56), which flies one dot per open ask from the spout to that point on a low arc. The original design (hydrant.ts:2-4) had asks \"settle at the Secretary\"; Mitchell has now asked for the opposite.\n\nDo, in one PR against main:\n1. Drop the Secretary as the target. In renderer.ts drawStream, remove secretaryOf/desk lookup for the stream; the water goes from the spout (the `beside(hydrant, TILE.HYDRANT, ...)` point) on a short, clearly visible arc (about one tile out and half a tile up, landing on the ground tile in front of / beside the hydrant, away from the Town Hall wall and not on the Secretary).\n2. Draw a small pool where the arc lands: a flat water-blue ellipse (a few px high, ~one tile wide at most) in the same #7cc4ff family, slightly darker/translucent, drawn before the dots so dots land on it. Let the pool's width grow a little with the open-ask count (e.g. 4 px at 0 asks up to ~T px at MAX_PARTICLES) so the hydrant still reads as \"how much is waiting\" without text. With 0 asks the pool may still show as a tiny puddle so the arc's landing place stays obvious; no dots then (keep the reduced-motion rule: no dots, pool static).\n3. Keep streamParticles pure and tested: update its unit test (grep for streamParticles in packages/web test files) and add one for the pool size helper. Update the header comments in hydrant.ts and the drawStream doc comment, and the hydrant line in docs/legible-delegation.md §3 if it says the dots settle at the Secretary. Note the change in docs/log.d/<date>-hydrant-pool.md.\n4. Check it in the browser at desktop and phone size: the arc must not overlap the hydrant sprite or the Secretary, and must read as water from a hydrant. Attach a screenshot (upload it) in the report.\nPark with resumeWhen {pr: N, merge: true}. Verdict stop when merged; Mitchell hears via the Done notice. Report: what a human sees at the hydrant now, the PR number."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-20T01:38:56.386Z"
flagPos: {"x":73,"y":8}
pickedUpAt: "2026-11-20T01:38:11.575Z"
pickedUpBy: "ag_s1kuuuo54b"
createdAt: "2026-11-20T01:37:53.312Z"
updatedAt: "2026-11-20T01:38:56.386Z"
---
i don't understand why the water coming out of the fire hydrant is always pointing at the secretary? just make it do a little ark and form a small pool
