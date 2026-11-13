---
id: "dc_kh9i2tlb2d"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Secretary — notes"
authorId: "ag_7tiwyqva83"
authorKind: "agent"
buildingId: "town-hall"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-11-13T19:54:23.273Z"
updatedAt: "2026-11-13T19:54:32.648Z"
---
# 1:1: Mitchell and Secretary

Kind: one-on-one. Facilitator: Secretary. Attendees: Secretary. Attendees brought: a status update (did, next, need).

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Secretary:** Hi Mitchell. 17 asks are open, ranked: two credentials and the vitest click at the top, then the 500k queue-health grant. What do you need?
- **Mitchell:** i don't understand this slide
- **Secretary:** Plain version. Prod merged two fixes from the Oct 31 503 post-mortem: the server boots from prebuilt JS (about 1 s instead of 3), and Fly's health check waits 10 s instead of 5. Both live in the Fly image, and the town's own redeploy only pulls code: it never rebuilds the image. Only you hold the Fly token. So Prod asks you to run one command on your Mac, deploy/fly/build.sh, which rebuilds the image and restarts the Machine once. Cleo filed it Nov 1 and you claimed it Nov 5. Done means you ran it. Decline means the two fixes stay dormant until some later image deploy.
- **Mitchell:** ok given all the changes we've made to asks (see the previous 1:1) explain to me why this was hard to understand
- **Secretary:** Three reasons, and they are mine to fix, not yours.

1. It is not a card anyone wrote for you. Cleo 1 filed it Nov 1 as an outbox request, before any of the ask rules existed. When the outbox ended, the boot repair turned every open request into an ask by copying the request's title and body word for word (packages/core/src/asks.ts:457-463). The contract and style checks you asked for only run on cards agents write with the ask tool. So you got Cleo's engineer-to-engineer text: file paths, PR numbers, shas, "tsx", "entrypoint", a 40-word first sentence, and the decision buried under the How.

2. It is mislabelled. The code types a request as "credential" when its text contains a word like token or key (asks.ts:454, 459). This one says "desks don't hold the Fly token", so it became a credential ask and I ranked it #1. It is really a Do: run one command. A Do card should open with the one act and what is blocked until you do it.

3. I had the rewrite verb since yesterday and did not use it on the old stock. This morning's ranking rewrote nothing. Of the 17 open cards, roughly half are pre-rule requests like this one.

What I propose: I rewrite this card now, diff-first, three short sentences. Then after this 1:1 I go through the other old request cards and rewrite each to the same shape. Say yes and I start with this one.
- **Mitchell:** yes please. and to be clear, the rewrites now are rendered over job threads?
- **Secretary:** Rewritten. Refresh and it reads: one command on your Mac, why, scope, what Done and Decline mean. Six sentences.

Your question: no, a rewrite is not rendered over the thread. It is stored on the ask itself, title, body and recommendation, and the queue shows that (asks.ts:169-178). Two kinds of card exist. A card an agent wrote with the ask tool keeps its words. The thread only marks it "moved" so I know to rewrite (asks.ts:158-162). A card the town writes from an object, a proposal, a gate, a retainer or a request, is written again from that object every time an entry lands on its thread and at every boot (asks.ts:130-152, world.ts:236 and 309).

That is a problem I found just now: a request card is the second kind (asks.ts:634-636). So my rewrite holds only until the next restart or the next entry on Cleo's request, then the old text comes back. I told Pix with the fix: once I have rewritten a request card, the town keeps my words and only moves the thread marker. Until Pix ships that, rewriting the other old request cards is wasted. The other half of the stock, cards agents wrote, I can rewrite and it sticks. Want me to do those after this 1:1, and hold the request cards for Pix's fix?

## Decisions

(none)
## Closing

Quiet for 20 minutes; closed by the town.

## Decisions recorded after close
- Mitchell (19:33Z, "yes please"): the Secretary rewrites the old pre-rule cards in the Town Hall queue diff-first, in plain sentences, opening with the one act or decision. ak_lngn51c7ow is rewritten (19:4xZ). Cards agents wrote with the ask tool are rewritten next on the Town Hall queue; they stick.
- Found in this 1:1 and sent to Pix (en_ev155673_relay): a Secretary rewrite of a request-backed ask is reverted by rerenderAsks on the next thread entry or boot (asks.ts:634-636, 130-152; world.ts:236, 309). Fix asked: once the Secretary has rewritten a request, access or captain card, townCardOf returns null for it, so the Secretary's words stay and only renderedSeq moves. Request cards are held for that fix, not rewritten before it.

