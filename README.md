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
| M | Map & objectives |
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

## Built with

- [Three.js](https://threejs.org/) r128 (loaded from CDN)
- Designed and written with Claude ([Anthropic](https://www.anthropic.com))

## Credits & licenses

- **Environment & mech art** — [Quaternius](https://quaternius.com) (CC0: mechs, drone, weapons, sci-fi environment, garden trees)
- **Skeleton characters** — "KayKit Character Pack: Skeletons" by [Kay Lousberg](https://kaylousberg.itch.io) (CC0)
- **Textures** — [Kenney](https://kenney.nl) (CC0)
- **Rover** — "SCI-FI Low-Poly Rover" by Corvin12
- **Guide characters** — avatars made with [Ready Player Me](https://readyplayer.me); animations from [Mixamo](https://www.mixamo.com) (Adobe). Mixamo assets are included only as needed to run this game; they may not be extracted and redistributed on their own.
- **Music** — streamed from [OpenGameArt](https://opengameart.org), credited in-game per track
- **Voices** — generated with Gemini TTS
- The games behind the doors (HexGL, Trigger Rally, and my own) live in their own
  repositories/hosting with their own licenses — none of their code or content is
  included here. "HexGL" by Thibaut Despoulain (MIT); "Trigger Rally" © Code Artemis (GPL v3).

Code of this hub: © Lightsmith Forge. Free to play; if you'd like to reuse the code,
open an issue and ask.
