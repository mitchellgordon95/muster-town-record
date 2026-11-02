---
id: "dc_vaaqyc943b"
type: "meeting-notes"
state: "building"
title: "1:1: Mitchell and Pix — notes"
authorId: "ag_mh0qidzgw6"
authorKind: "agent"
buildingId: "workshop"
provenance: {"sourceIds":[],"urls":[]}
tags: []
createdAt: "2026-10-25T18:02:45.941Z"
updatedAt: "2026-10-25T18:02:45.941Z"
---
# 1:1: Mitchell and Pix

Kind: one-on-one. Facilitator: Pix. Attendees: Pix.

## Agenda

(none)

## Summaries

(none)
## Discussion

- **Pix:** Hi Mitchell. Grant gr_jqsqra0dlx is re-proposed at 24M and waiting on you in the Town Hall in-tray; KR1–3 work is queued and starts on funding. What do you need?
- **Mitchell:** do you have access to our previous 1:1?
- **Pix:** Yes, the notes are filed ([dc_bo7xuobtbv](2026-10-25-1-1-mitchell-and-pix-notes-7xuobtbv.md)). I also see I went silent on your last message there, sorry; the session was cut by the queued redeploy. Where we left off: (1) a human writes goals and their KRs, with the manager assisting; (2) a grant names one KR, and the old grant-level KRs become a testing plan on the grant; (3) no to moving the three Workshop KRs onto the goal yet, we still need to discuss goals; a building with no KRs to explore against and no funded grants should show as blocked, and the manager should proactively chase human decisions to unblock it; (4) on the grant, "do whatever works". Nothing from that has been assigned yet, and my 16:58 re-proposal of gr_jqsqra0dlx at 24M predates acting on it, so it still uses the old model. Want to settle the Workshop's KRs now, or should I first assign the model change (KRs on the goal, grant names a KR, blocked state + manager nudges) and come back to you with proposed KRs?
- **Mitchell:** for now let's just focus on the model change

also we should probably fix meeting resume on redeploy. if a meeting response is blocked by redeploy it should also say that in the meeting
- **Pix:** Done, three assignments, all exploration lane:
- Lena (as_6ggmieufpu): the core model change. KRs on the building goal, human-written with the manager assisting; a grant names one KR and carries the plan, its old KRs become a testing plan; lanes, checkpoints and the board read KRs off the goal; a building with no KRs and no funded grant shows blocked and wakes the manager once to go get human decisions. Migration keeps gr_jqsqra0dlx's three KRs as its testing plan with no goal KR yet, so the Workshop will correctly show blocked until you write its KRs.
- Root (as_tatcakwm1m, waits for Lena): the UI. KR editor in Building → Settings, grant forms pick and show the KR, blocked badge on building, map and Town Hall in-tray.
- Keel (as_tmqcmufeup): meetings survive a redeploy. A transcript line saying the reply is waiting on the redeploy, the facilitator's session resumes after the restart and answers what it missed, and the drain stops waiting indefinitely on meeting sessions.
I'm leaving gr_jqsqra0dlx proposed as is; it gets re-shaped onto a goal KR once we discuss the Workshop's KRs. Anything else?

## Decisions

1. Model change, core: KRs live on the building goal (human-written, manager assists); a grant names one KR and carries the plan, its former KRs become a testing plan; lanes, checkpoints and the board read KRs off the goal; a building with no KRs and no funded grant is blocked and wakes the manager once to get human decisions. Lena owns core/schema/API/docs. → Lena
2. Model change, web UI: humans edit goal KRs in Building → Settings; grant forms name one KR and show the testing plan; blocked badge on building, map and Town Hall in-tray; board KR view reads the goal. Root owns, after Lena's core lands. → Root
3. Meetings survive a redeploy: a system line in the transcript when a reply is blocked by a pending redeploy, the facilitator's session resumes after the restart and answers what it missed, and the drain no longer waits indefinitely on meeting sessions. Keel owns. → Keel

