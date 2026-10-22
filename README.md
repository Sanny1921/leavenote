# LeaveNote

Stop coding when you want. Paste your `git diff` (plus an optional one-line note about what you were doing), and a local open-weight model writes the handover note that gets tomorrow-you back up to speed: what changed, what's unfinished, the first thing to do next, and what to watch out for.

Built for Hacktoberfest 2026, DEV Open-Source AI Challenge, Week 3: **Slow and Steady** - it does the boring context-reloading work so you don't have to.

## How it runs

- Fully in the browser. The model (Qwen2.5-0.5B-Instruct, Apache 2.0) is downloaded once and cached; inference happens on your device via [WebLLM](https://github.com/mlc-ai/web-llm) (Apache 2.0).
- No server, no API key, no account, no analytics. Your code never leaves your device.
- Requires WebGPU (recent Chrome/Edge on a device with a supported GPU). Devices without it get an honest message; nothing is faked.
- Long diffs are trimmed to the first 1600 characters (small model, small context). Paste the part tomorrow-you most needs.

## Files

- `index.html` - the whole app (UI + logic)
- `worker.js` - WebLLM web worker

## Run locally

Any static server works, e.g. `npx serve .` - then open the page in a WebGPU-capable browser.
