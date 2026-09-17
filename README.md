# The Arrivals Hall

**▶ Play it here: https://code-4you.github.io/arrivals-hall/**

Also playable on [itch.io](https://freegames99.itch.io/arrivals-hall) and at the home site, [Lightsmith Forge](https://lightsmithforge.linkpc.net/hub/).

A first-person walkable 3D hub — a small sci-fi mall that is the arrivals hall of a
human–AI community. Each door launches one of my games (hosted on the Lightsmith Forge
site). Talk to Elara the guide, tell the fountain what you want to do, write on the
ideas wall, or listen to short stories performed by the characters. Early build —
expect rough edges.

## Controls

| Key | Action |
|---|---|
| WASD | Walk |
| Mouse | Look around |
| E | Interact / enter a game |
| Shift | Jog |
| Space | Jump |
| M | Map & tracking |
| Esc | Free the cursor |

Best on desktop with a keyboard. The doors navigate to games hosted on
lightsmithforge.linkpc.net — use your browser's back button to return.

## Running it yourself

It's a single static page — no build step. Serve the folder with any static server, e.g.:

```
python -m http.server 8080
```

then open http://localhost:8080/. (Opening index.html straight from disk won't work —
browsers block model/JSON fetches from `file://`.)

The ideas wall, play counts, save keys, and the Elara chat talk to a small PHP + MySQL
backend on lightsmithforge.linkpc.net (`account/api.php`, `account/gemini.php`, CORS `*`);
without it the page still runs and falls back to local storage and browser voices.

## Add your level or your game

The six floors above the hall and the Arcade's posters are for visitors' work. Ask Claude Code, ChatGPT Desktop
or any coding assistant to do it from this repository — paste it **https://code-4you.github.io/arrivals-hall/contribute.html**
and it will know what to do: get the code, run it, add your level or game, show it live on your own GitHub Pages, and
open a pull request. The same text is in [CONTRIBUTING.md](CONTRIBUTING.md); what the licence allows for this is in
[LICENSE.md](LICENSE.md), sections *You may* and *Contributing*.

## Built with

- [Three.js](https://threejs.org/) r128 (loaded from CDN)
- Designed and written with Claude ([Anthropic](https://www.anthropic.com))

## Credits & licenses

- **Environment & mech art** — [Quaternius](https://quaternius.com) (CC0: mechs, drone, weapons, sci-fi environment, garden trees)
- **Skeleton characters** — "KayKit Character Pack: Skeletons" by [Kay Lousberg](https://kaylousberg.itch.io) (CC0)
- **Textures** — [Kenney](https://kenney.nl) (CC0)
- **Rover** — "SCI-FI Low-Poly Rover" by Corvin12
- **Elara** — body "Cat Woman", face capture "Facial animation of a sexy girl" and standing capture "Dahlia", all by [patromes](https://sketchfab.com/patromes) on Sketchfab (CC BY 4.0); gesture animations from [Mixamo](https://www.mixamo.com) (Adobe) — included only as baked into this game, not to be extracted and redistributed on their own; extra idles from the "Universal Animation Library" by [Quaternius](https://quaternius.com) (CC0).
- **Music** — streamed from [OpenGameArt](https://opengameart.org), credited in-game per track
- **Voices** — generated with Gemini TTS
- The games behind the doors (HexGL, Trigger Rally, and my own) live in their own
  repositories/hosting with their own licenses — none of their code or content is
  included here. "HexGL" by Thibaut Despoulain (MIT); "Trigger Rally" © Code Artemis (GPL v3).

## License

© Lightsmith Forge — **source-available, not open source**: free to play, to read, and to edit for your own
personal, non-commercial use, and contributions are welcome (see above); no commercial use, re-hosting, or use as
AI training data without permission. See [LICENSE.md](LICENSE.md).
Third-party assets keep their own licenses (details there).
