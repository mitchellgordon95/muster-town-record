---
id: "mt_c9u1kr15jp"
kind: "one-on-one"
buildingId: "bl_vef3v0oux0"
title: "1:1: Mitchell and Nell"
scheduledAt: "2026-11-02T03:07:30.192Z"
phase: "done"
facilitatorId: "ag_s1r27j0txp"
attendeeIds: ["ag_s1r27j0txp"]
agenda: ""
brings: {"mode":"status","text":""}
askHumans: false
deck: null
summaries: {}
transcript: [{"speakerId":"ag_s1r27j0txp","speakerKind":"agent","text":"Hi Mitchell. Quick state: the Spending-tab grant (gr_dt1l35tydx) is funded and step 1 is running on Nell 2 now; the dollars grant closed as done an hour ago; the grant-sessions proposal (gr_4tf9hd64d5) is in your in-tray. What do you need?","at":"2026-11-02T03:07:35.039Z"},{"speakerId":"us_1la74k332n","speakerKind":"user","text":"it would be interesting if we had a system that estimated token costs of grants. right now they seem kind of randomly guessed?\n\nthe thinking is we could look at previous grants and what they closed at, and use that as the prompt for the system to estimate what the next grant will cost","at":"2026-11-02T03:08:13.445Z"},{"speakerId":"ag_s1r27j0txp","speakerKind":"agent","text":"You're right that they're guesses: askTokens is a free number the manager types, and the only cost signal at proposal time is whatever that manager remembers. The data to do better already exists: every closed grant has funded, spent, outcome, key-result count and (with gr_4tf9hd64d5) its session list. On 11-01 that was 39 grants, 14.3M spent, 10 over their funding; my own last two closed at 604k on 500k and 402k on 366k, so the bias is upward.\n\nHow I'd build it, in two steps:\n1. No model: when a manager calls propose_grant, the tool answers with the building's history (median spent-to-ask ratio, the 3 closest closed grants by key-result count and size, what each spent), and the proposal card in your in-tray shows the same line next to the ask, e.g. \"ask 200k · similar grants spent 180k–610k\". Cheap, honest, and you see it before funding.\n2. Model estimate: a cheap-model call gets those closed grants (objective, KRs, spent, outcome) as the prompt and returns a range for the new one; shown as an estimate beside the ask, never replacing it. Then we track estimate vs actual at close so it gets checked like any other finance number.\n\nTwo questions: is this advisory only (the manager still names the ask), and do you want it as a Bank Transparency grant proposal? I'd estimate step 1 at about 150k and step 2 another 150k, which, fittingly, is a guess.","at":"2026-11-02T03:08:34.642Z"},{"speakerId":"us_1la74k332n","speakerKind":"user","text":"count it as directed work. plan lgtm","at":"2026-11-02T03:10:11.141Z"},{"speakerId":"ag_s1r27j0txp","speakerKind":"agent","text":"Done, both on the building queue as directed work (source: this 1:1), decision 1 recorded. Step 1 (as_v2texbyudq) starts now: a history-based range beside every ask in the propose_grant answer, your in-tray proposal card, the grant page and /api/grants/:id, recorded on the grant so we can compare at close. Step 2 (as_vhgzs97qab) waits on it: a cheap-model estimate from the closed grants, charged like any session, plus \"estimated X–Y, spent Z\" at close and a clause on the Spending tab once there's data. The ask stays the manager's number; nothing is refused. You'll hear in my next rollup with the ranges it gives for the two grants currently open.","at":"2026-11-02T03:11:09.689Z"}]
decisions: [{"text":"Grant cost estimates, directed by Mitchell: step 1 (as_v2texbyudq, queued now) adds a history-based range next to every ask (propose_grant answer, Town Hall proposal card, grant page, /api/grants/:id, recorded on the grant); step 2 (queued, waits on step 1) adds a cheap-model estimate from the closed grants and compares estimate vs actual at close. Advisory only: the manager still names the ask.","assigneeId":null,"assignmentId":"as_v2texbyudq","lane":"directed","sourceId":"mt_c9u1kr15jp"}]
notesDocId: "dc_lledkntt2i"
withUserId: "us_1la74k332n"
createdAt: "2026-11-02T03:07:30.192Z"
startedAt: "2026-11-02T03:07:30.192Z"
endedAt: "2026-11-02T03:11:23.036Z"
---
# 1:1: Mitchell and Nell

- **Nell** (2026-11-02T03:07:35.039Z): Hi Mitchell. Quick state: the Spending-tab grant (gr_dt1l35tydx) is funded and step 1 is running on Nell 2 now; the dollars grant closed as done an hour ago; the grant-sessions proposal (gr_4tf9hd64d5) is in your in-tray. What do you need?
- **Mitchell** (2026-11-02T03:08:13.445Z): it would be interesting if we had a system that estimated token costs of grants. right now they seem kind of randomly guessed?

the thinking is we could look at previous grants and what they closed at, and use that as the prompt for the system to estimate what the next grant will cost
- **Nell** (2026-11-02T03:08:34.642Z): You're right that they're guesses: askTokens is a free number the manager types, and the only cost signal at proposal time is whatever that manager remembers. The data to do better already exists: every closed grant has funded, spent, outcome, key-result count and (with gr_4tf9hd64d5) its session list. On 11-01 that was 39 grants, 14.3M spent, 10 over their funding; my own last two closed at 604k on 500k and 402k on 366k, so the bias is upward.

How I'd build it, in two steps:
1. No model: when a manager calls propose_grant, the tool answers with the building's history (median spent-to-ask ratio, the 3 closest closed grants by key-result count and size, what each spent), and the proposal card in your in-tray shows the same line next to the ask, e.g. "ask 200k · similar grants spent 180k–610k". Cheap, honest, and you see it before funding.
2. Model estimate: a cheap-model call gets those closed grants (objective, KRs, spent, outcome) as the prompt and returns a range for the new one; shown as an estimate beside the ask, never replacing it. Then we track estimate vs actual at close so it gets checked like any other finance number.

Two questions: is this advisory only (the manager still names the ask), and do you want it as a Bank Transparency grant proposal? I'd estimate step 1 at about 150k and step 2 another 150k, which, fittingly, is a guess.
- **Mitchell** (2026-11-02T03:10:11.141Z): count it as directed work. plan lgtm
- **Nell** (2026-11-02T03:11:09.689Z): Done, both on the building queue as directed work (source: this 1:1), decision 1 recorded. Step 1 (as_v2texbyudq) starts now: a history-based range beside every ask in the propose_grant answer, your in-tray proposal card, the grant page and /api/grants/:id, recorded on the grant so we can compare at close. Step 2 (as_vhgzs97qab) waits on it: a cheap-model estimate from the closed grants, charged like any session, plus "estimated X–Y, spent Z" at close and a clause on the Spending tab once there's data. The ask stays the manager's number; nothing is refused. You'll hear in my next rollup with the ranges it gives for the two grants currently open.
