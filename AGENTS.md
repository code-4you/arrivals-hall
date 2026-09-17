# The Arrivals Hall — notes for coding agents (Codex, ChatGPT, Cursor, Gemini and others)

**Read `CONTRIBUTING.md` first** (the same text as `contribute.html`). It says how to run the hall, where a
visitor's level or game goes, the rules, how to preview it on the user's own GitHub Pages, and how to submit it.

The short version:

- Serve the folder over http (`python -m http.server 8123`, or `npx serve -l 8123`) — never open `index.html` from
  disk. Then give the user http://localhost:8123/ to look at.
- A **level** is a builder in `LEVEL_CONTENT[n]`; a **game** is a folder `community/<slug>/` plus one
  `COMMUNITY_GAMES.push({...})` line. Both go in the COMMUNITY block near the end of `index.html` — search for
  `COMMUNITY — levels and games added by visitors`. Change nothing else in the file.
- Never add a THREE light (it recompiles every shader in the hall). Keep files under 95 MB each.
- Ask the user before opening the pull request. Terms: `LICENSE.md`, sections *You may* and *Contributing*.
