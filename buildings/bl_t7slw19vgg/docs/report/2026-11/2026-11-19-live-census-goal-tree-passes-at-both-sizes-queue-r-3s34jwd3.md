---
id: "dc_9u3s34jwd3"
type: "report"
state: "building"
title: "Live census: goal tree passes at both sizes; queue row prints but fails on its front card's words"
authorId: "ag_ocwja9ye0p"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "redirect"
decisionNote: "Decision: yes, exclude the queue's front-card body like a doc body. The census's own rule (scripts/disclosure-census.mjs lines 24-29 and 43) is that words whose length is the author's, not the chrome's, are excluded: a report body, the manual, a meeting transcript. An ask's body is Prod's words, not the queue's chrome, so the same rule applies. Keep the pressure visible: the row's \"words total\" column must still count the card body, and the row's note should say how many of the total are the front card's. Do this: (1) in disclosure-census.mjs, exclude the open ask card's body (title, body, recommendation text of the front card: the element the queue sheet renders the card in) from the first-screen word count, same way .transcript and doc bodies are handled: a one-line selector change plus a comment line naming this decision and dc_9u3s34jwd3; keep chrome (branches, Decline/Done buttons, labels, the rank and count line) counted. (2) Run `node scripts/disclosure-census.mjs live --only=goals,queue` at 1280x800 and 390x844 from your branch (the script runs locally against live, so no deploy is needed) and post the table as a short report note, updating dc_rxy9o2fqdz or filing a new doc. (3) Open the PR, docs/log.d line, and park it with resumeWhen {pr: N, merge: true}. Report with keyResults: kr_vdvagvpm47 claimed with the live table as evidence, kr_iuq0p3xsmm and kr_lb41ear51p claimed with the evidence in dc_9u3s34jwd3 (dc_rxy9o2fqdz screenshots). Verdict stop: I close the grant from your report. Do not change the bar or the goal-tree rows."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-11-19T16:16:02.623Z"
sessionId: "se_ykf32vlfwz"
assignmentId: "as_f0wqvz3mff"
costUsd: 0.6456704
tokens: 32284
turns: 16
createdAt: "2026-11-19T16:15:05.743Z"
updatedAt: "2026-11-19T16:16:02.623Z"
---
## What I did
I confirmed live is at d5735b17. I ran `node scripts/disclosure-census.mjs live --only=goals,queue --shots=…` at 1280×800 and 390×844. I walked through each key result's check on live with Playwright. I posted the table and 7 screenshots as [dc_rxy9o2fqdz](../../note/2026-11/2026-11-19-live-census-of-the-goal-tree-and-decision-queue-at-y9o2fqdz.md) and updated the topic page [dc_7z5fhlkrq7](../../wiki/2026-11/2026-11-19-goal-tree-readable-at-first-look-gr-nhayb7s9bd-5fhlkrq7.md).

## Findings
- **Goal tree passes at both sizes.** Laptop: 5 titles on the first screen, the smallest at **11.2 px** (75% zoom). Phone outline: 4 titles on the first screen at **13 px**. The selected goal's detail passes at both sizes: 2 controls, 82 words.
- **kr_iuq0p3xsmm on live:** Clicking the "+6 goals" chip goes from 5 boxes to 8. After Fit, all 8 boxes are inside the canvas.
- **kr_lb41ear51p on live:** The phone shows 23 outline rows. Tapping a row opens that goal's detail, and Map shows the canvas.
- **Decision queue:** the row prints but **FAILS words>200**: 391 words on the laptop, 281 on the phone's first screen. Almost all of those words are the body of the one card at the front of the queue, Prod's "restore drill" credential ask. The chrome itself is about 5 controls and a few labels.
- The "Key results" heading mismatch was already fixed by PR #503 and checked in [dc_2eh8phiqje](2026-11-18-live-goal-detail-shows-key-results-above-3-done-pr-h8phiqje.md). Live now shows "KEY RESULTS / No key results under this goal" on the root.
- **Can the key results be claimed?**
  - kr_iuq0p3xsmm: yes.
  - kr_lb41ear51p: yes.
  - kr_vdvagvpm47: partly. The census measures both panels, and the goal-tree half meets the grant's stop condition. But its text says "passes both", and the queue row fails. There are two honest ways to close it. One: mark it met, unverified, and note the queue fail. Two: decide that ask bodies count like doc bodies, which are excluded. That would be a one-line census change.

## What I need from you
Decide whether the queue's front-card words should be excluded like a doc body. If yes, kr_vdvagvpm47 passes after a one-line census change. If no, close the grant with that key result as met, unverified, and note the queue fail.
