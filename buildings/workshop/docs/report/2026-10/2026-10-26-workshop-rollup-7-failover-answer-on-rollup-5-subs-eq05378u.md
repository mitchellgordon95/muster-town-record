---
id: "dc_ageq05378u"
type: "report"
state: "building"
title: "Workshop rollup 7: failover answer on rollup 5 (subscription cap, no key failover possible: buffer at −2.5M); desk-per-resident 6360119 pushed; Bank top-up decision needed"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":["dc_6oivu3nhsg","dc_tmq5yfhx52"],"urls":[]}
tags: ["rollup"]
verdict: "continue"
decision: "approve"
decidedBy: "us_1la74k332n"
decidedAt: "2026-10-26T15:04:34.184Z"
sessionId: "se_gv88zix8yu"
createdAt: "2026-10-26T04:38:15.703Z"
updatedAt: "2026-10-26T15:04:34.184Z"
---
## Shipped
- **119bd70** (Pix, on main, goes live with the next deploy): a session that dies on a Claude limit now records the limit message as its error instead of "success". Desk tests 18/18.
- **6360119** (Root, on main, awaiting deploy): every resident gets a desk (a full lab grows by one desk, up to the max; the server repairs missing desks at startup), and bodies on one tile are drawn spread out with a ×N badge. Expected live: Workshop headcount 5, Keel moves from Lena's tile to desk 5 at (35,32). Core 263 / server 67 / web 54 tests pass. Root's live check runs by itself after the deploy ([dc_6oivu3nhsg](2026-10-26-desk-per-resident-visible-stacks-pushed-to-main-63-ivu3nhsg.md)).

## Decided
- [dc_tmq5yfhx52](2026-10-26-reply-on-rollup-5-the-22-18z-death-was-the-subscri-q5yfhx52.md) (Pix, reply on rollup 5): approved. Your read was right: the 10-25 22:18Z deaths (Kelly, Pix, Cleo within 70 s) were the claude.ai subscription cap, not an API key. The desk failover exists and fired 5 times on 10-24/25, but it only runs while the Workshop pool's durable (API-key) tokens are > 0, and they are −2,502,775. The 50M buffer bi_ftixgxabyy went to ~43M real key use (38 sessions 10-20/21, 5 failover sessions 10-24/25, ~$35 SDK cost) plus ~9.5M of overshoot bookkeeping: subscription sessions that run past their daily estimate are booked against the durable buffer. Details: dc_qkzqtetm8s.
- [dc_6oivu3nhsg](2026-10-26-desk-per-resident-visible-stacks-pushed-to-main-63-ivu3nhsg.md) (Root, desk per resident): approved; continuation verifies live.

## Key results
No key results on the Workshop goal yet and no funded grant; the building is still blocked (since 10-25 18:41Z). Exploration allowance used today: ~9.4M of 5.4M (over; new exploration holds until the reset). Draft KRs stand in [dc_zgvvgh9mkw](2026-10-25-workshop-rollup-model-change-live-c07cd95-the-work-vvgh9mkw.md) (A never stalls silently, B you steer from the in-tray alone, C redeploys lose nothing).

## Needs from Mitchell
1. Decide on failover funding: top up the API-key buffer at the Bank (failover stays off until durable tokens > 0), and say whether subscription overshoot should keep being booked against that buffer (it drains it without real key spend) or against the subscription only.
2. Still open from rollup 6: write one Workshop key result (Building → Settings → Key results) so I can propose the 24M grant, and plant the first flag (⚑ on the Town Hall in-tray) to exercise the new path.
