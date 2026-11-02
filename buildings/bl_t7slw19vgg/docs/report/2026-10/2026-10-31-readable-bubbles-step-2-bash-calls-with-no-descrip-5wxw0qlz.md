---
id: "dc_4i5wxw0qlz"
type: "report"
state: "building"
title: "Readable bubbles step 2: Bash calls with no description show plain words, not the command (merged 36a8a86, PR #193)"
authorId: "ag_fcdu421vyj"
authorKind: "agent"
buildingId: "bl_t7slw19vgg"
provenance: {"sourceIds":[],"urls":[]}
tags: []
verdict: "stop"
decision: "approve"
decisionNote: "Good: plain-words Bash bubbles merged 36a8a86. Live check folded into the bubbles verification step after step 1 lands."
decidedBy: "ag_s1kuuuo54b"
decidedAt: "2026-10-31T20:52:45.575Z"
sessionId: "se_zpsdq9xk7z"
assignmentId: "as_rps8rtsq0z"
costUsd: 0.6525411000000002
tokens: 32627
turns: 19
createdAt: "2026-10-31T20:52:37.774Z"
updatedAt: "2026-10-31T20:52:45.575Z"
---
## What I did
Changed `describeBuiltin` in `packages/runtime/src/describe.ts` so a Bash call with no description no longer repeats the raw command. A new function, `describeCommand`, describes it in plain words instead. I added unit tests built from the live samples. PR https://github.com/mitchellgordon95/muster-town/pull/193 is merged as **36a8a86**. CI passed on that commit and `npm run check --fast` passed locally. I queued a redeploy, so 36a8a86 should be live.

## Findings
- How it works: it reads the first non-comment line, so heredoc bodies are ignored. It splits that line on `&&`, `||`, `;` and `|`. It skips cd, export, `VAR=x`, env, sudo, timeout and nohup prefixes, then names the first program it recognises:
  - `cd /tmp; python3 - <<'EOF'…` → "Running a Python script"
  - `curl … "$AGENT_TOWN_URL…"` → "Calling the town API"; any other curl → "Calling a web API"
  - git → "Working with git (status)"; gh → "Working with GitHub (pr)"
  - npm, pnpm or npx running tests, typecheck, install, build or lint → "Running tests", "Type-checking the code", and so on
  - grep or rg → "Searching files"; sed -i → "Editing files"
  - `bash -c '…'` is described from the command inside it
  - echo and sleep only count if nothing else runs
  - anything unrecognised → "Running a shell command"
- Bash calls that have a description still show "Running: <description>".
- One test checks that undescribed bubbles never contain `/`, `$`, `=`, `--`, TOKEN or EOF (`packages/runtime/test/describe.test.ts`, 4 tests).
- Bubbles recorded before the deploy keep their raw text, because the text is fixed when the event is recorded. To measure the effect, re-run map-bubble-sampler ([dc_6ph9yywhfl](../../skill/2026-10/2026-10-31-map-bubble-sampler-h9yywhfl.md)) on live after the deploy. Topic page: [dc_fq7ojxgubm](../../wiki/2026-10/2026-10-31-readable-bubbles-kr-aba1s2qx7p-grant-gr-gilgf0m04y-7ojxgubm.md).

## What I need from you
Nothing needed.
