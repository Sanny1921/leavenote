# LeaveNote

Stop coding when you want. Paste your `git diff` (plus an optional one-line note about what you were doing), and a local open-weight model helps write the handover note that gets tomorrow-you back up to speed: what changed, what's unfinished, the first thing to do next, and what to watch out for.

Built for Hacktoberfest 2026, DEV Open-Source AI Challenge, Week 3: **Slow and Steady** - it does the boring context-reloading work so you don't have to.

## How it runs

- Fully in the browser. The model (Qwen2.5-0.5B-Instruct, Apache 2.0) is downloaded once and cached; inference happens on your device via [WebLLM](https://github.com/mlc-ai/web-llm) (Apache 2.0).
- No server, no API key, no account, no analytics. Your code never leaves your device.
- Requires WebGPU (recent Chrome/Edge on a device with a supported GPU). Devices without it get an honest message; nothing is faked.
- Long diffs are trimmed to the first 1600 characters (small model, small context). Paste the part tomorrow-you most needs.

## How it works (v2, lightweight)

A small model is bad at judging a raw diff - it can call unfinished work done. So LeaveNote splits the job:

1. **Plain code reads the diff first**: file names, added/removed line counts, leftover `TODO`/`FIXME` markers, and debug lines (`console.log`, `debugger`).
2. **UNFINISHED and WATCH OUT always come from that direct reading** - never from the AI - so those sections cannot contradict your actual diff.
3. **The AI only writes the two lines it is good at**: a plain-English summary of what changed (CHANGED) and a suggested first step for tomorrow (START TOMORROW), phrased from the facts it is handed. If its answer fails the format or sanity checks, that line falls back to a parsed version and the note's footer says exactly which lines are AI-written and which are parsed.

The prompt pipeline was validated against the real Qwen2.5-0.5B-Instruct weights on CPU: 3/3 test diffs produced the required format, and the checks reject "nothing to do" answers when the diff still contains flagged TODOs.

## Files

- `index.html` - the whole app (UI + logic)
- `worker.js` - WebLLM web worker

## Run locally

Any static server works, e.g. `npx serve .` - then open the page in a WebGPU-capable browser.

Live demo: https://leavenote-app.netlify.app
