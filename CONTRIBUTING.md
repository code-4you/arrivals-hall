# Add your level or your game to The Arrivals Hall

The Arrivals Hall is a walkable 3D mall that lives in one HTML file. Its source is on GitHub — a synced copy of the live hall. A visitor can add a **level** (one of the six empty floors above the hall, reached by the elevator) or a **game** (a browser game of your own, hung on a poster in the Arcade room), look at it live, and submit it to be hung in the real hall.

> **If you are a person:** you do not need to code. Open Claude Code, ChatGPT Desktop or any coding assistant that can run commands, paste the address of this page and say what you want — for example *"Follow this page and add a level with a garden and a lookout"* or *"Follow this page and add my game from the folder on my desktop"*. Everything below is written for the assistant.

> **If you are an assistant** (Claude Code, ChatGPT Desktop / Codex, Cursor, Gemini CLI, or another): do the steps in order. After step 2 tell the user the local address to look at; after step 5 the public one; ask them before step 6, the submission. The same text is in the repository as `CONTRIBUTING.md`, and the terms you are working under are in its `LICENSE.md` (section *Contributing a level or a game*).

Repository: https://github.com/code-4you/arrivals-hall — Live copy: https://code-4you.github.io/arrivals-hall/ — Home site: https://lightsmithforge.linkpc.net/hub/

## 1. Get the code

You need `git`, Python 3 or Node for a local web server, and — for the preview address and the submission — a GitHub account for the user. Fork first, so there is somewhere to push to and to open the pull request from.

- The user forks it on GitHub: https://github.com/code-4you/arrivals-hall/fork (one click, *Create fork*). Then:

```bash
git clone https://github.com/<user>/arrivals-hall.git
cd arrivals-hall
```

- With the GitHub CLI, in one go: `gh repo fork code-4you/arrivals-hall --clone`
- No GitHub account yet? `git clone https://github.com/code-4you/arrivals-hall.git` gets everything (about 200 MB; *Code → Download ZIP* on the repository page works too). Fork later, for steps 5 and 6.

What you get: `index.html` — the whole hall in one file, about 7,000 lines, Three.js r128 loaded from a CDN; `assets/` — models, textures, voices; `local/` — bundled story data; `community/` — visitors' games, once there are some; `LICENSE.md`, `CONTRIBUTING.md`, `contribute.html`. A few Lab exhibits load from the home site and only for the official copy — on your copy those spaces stand empty. That is expected.

## 2. Run it, and give the user the address

There is no build step and nothing to install. Serve the folder over http — not `file://`, browsers block the model fetches from there:

```bash
python -m http.server 8123
```

(or `python3 -m http.server 8123`, or `npx serve -l 8123`). Then tell the user: **open http://localhost:8123/** — that is the hall, running from their copy. In the Claude Code desktop app the repository ships `.claude/launch.json`, so `preview_start` with the name `arrivals-hall` opens it in the app's browser.

Controls: WASD walk, mouse look, E interact, Shift jog, Space jump, M map, Esc menu. You arrive in the garden; the glass foyer is south of the hall, and E on the door at its north end opens the hall. The elevator stands in the foyer's west wall — buttons 1 to 6 are the levels.

## 3. Add a level

Everything a visitor adds goes in the **COMMUNITY block** near the end of `index.html` — search the file for `COMMUNITY — levels and games added by visitors`. Nothing else in the file needs to change, and nothing else may.

A level is a builder function stored under the level's number in `LEVEL_CONTENT`. It runs once, when the hall is built, inside that level's own zone, so what it adds is drawn only up there. Take the lowest level that has no entry in the block yet (if in doubt, take it and say so in the pull request).

```js
// ---- Level 2 — "Sky garden" by <name>, <date> ----
LEVEL_CONTENT[2]=function(Y,zn,B){
  const teal=new THREE.MeshStandardMaterial({color:0x5fe0c8,roughness:0.6});
  box(0,Y,0,3,1,3,teal,true);                                    // a solid block at x 0, z 0: 3 wide, 1 high, 3 deep — you can stand on it
  emissiveStrip(0,Y+3.9,10,6,0.1,0.3,0xffd27f,1.0);             // a glowing strip under the ceiling
  hotspot(0,3,2.2,'Read the plaque',()=>banner('WELCOME TO THE SKY GARDEN'));   // an E prompt at x 0, z 3
  new THREE.GLTFLoader().load('community/sky-garden/tree.glb',g=>{         // a model of your own
    g.scene.position.set(6,Y,-6); zoneTag(g.scene,zn); worldGroup.add(g.scene);
  });
};
```

What the builder is given:

- `Y` — the floor height. Feet stand at `y = Y`; the ceiling is at `Y + 4.2`. Place everything relative to `Y`.
- `zn` — the level's zone. Anything added *after* the builder returns — a loaded model, in its callback — needs `zoneTag(object, zn)` before `worldGroup.add(object)`, or it shows on every floor.
- `B` — the floor's extents, `{x0:-44, x1:44, z0:-44, z1:46}`. The elevator car stands at x −10.4, z 43.3 with its sign above it: keep three metres in front of it clear. Elara, the guide, rides up with the visitor and walks beside them, so leave paths at least two metres wide.

Helpers, all defined in `index.html`:

- `box(x, Y, z, width, height, depth, material, true)` — a solid block; `true` gives it collision, fixed to your floor automatically. Pass `false` for decoration.
- `emissiveStrip(x, y, z, width, height, depth, colour, intensity)` — a glowing box, the hall's light strips.
- `hotspot(x, z, radius, label, fn)` — an E prompt at a spot, shown only on your floor. `banner('TEXT')` puts a line on screen.
- `new THREE.GLTFLoader()` for `.glb` models; `THREE.CanvasTexture` for signs drawn on a canvas — `buildSubmitDesk` in the file is the pattern.
- Materials: `THREE.MeshStandardMaterial`. **Never add a THREE light** (PointLight, SpotLight …): one more light recompiles every shader in the hall and stalls it. Use emissive materials.

Keep it light: under 20 MB of files, under about 200,000 triangles, no more than a few dozen draw calls — the hall has to keep 60 fps on a laptop. Your own files go in `community/<slug>/`. Do not touch other people's blocks or anything outside the COMMUNITY block.

## 4. Add a game

A game is a folder `community/<slug>/` with an `index.html` that runs on its own — any engine: plain HTML and JavaScript, Three.js, Phaser, a Godot HTML export, Unity WebGL — plus one line in the COMMUNITY block:

```js
// ---- "Orbit Run" by <name>, <date> ----
COMMUNITY_GAMES.push({slug:'orbit-run', name:'Orbit Run', by:'<name>', blurb:'One line about it, shown on the poster.', url:'community/orbit-run/index.html'});
```

The Arcade room (north galleria, sign *ARCADE · COMMUNITY MAPS*) hangs a poster for each entry; E on the poster opens the game in the same tab, and every play is counted on the Leaders board. There are seven slots — if they are all taken, say so in the pull request.

Rules for the folder: relative paths only, inside your folder (it has to run from any address); no server side — GitHub Pages is static; every file under 95 MB (GitHub refuses larger ones) and the folder ideally under 100 MB; a way back is kind: `<a href="../../index.html">back to the hall</a>`.

## 5. Test it, then put it where the user can see it

Check locally first: reload http://localhost:8123/, open the hall, ride the elevator to your level or walk to the Arcade. Open the browser console — no red errors. Then push, and switch on GitHub Pages for the fork so the copy gets a public address:

```bash
git add -A
git commit -m "Add level 2: Sky garden"
git push
```

Pages: on GitHub, the fork → *Settings* → *Pages* → under *Build and deployment* choose *Deploy from a branch*, branch `main`, folder `/ (root)`, *Save*. With the CLI: `gh api -X POST repos/<user>/arrivals-hall/pages -f build_type=legacy -f "source[branch]=main" -f "source[path]=/"`. A minute or two later the copy is live at **https://<user>.github.io/arrivals-hall/** — tell the user that address. It is theirs to share; every push updates it.

## 6. Submit it

Ask the user first. Then open a pull request from the fork to `code-4you/arrivals-hall`, branch `main`:

- On GitHub: the fork's page shows *Contribute → Open pull request*.
- CLI: `gh pr create --repo code-4you/arrivals-hall --title "Add level 2: Sky garden" --body-file pr.md`

The description should say: what it is and where it hangs (the level number, or the Arcade); the Pages address where it can be tried; every third-party asset with its source and licence; the name to put on the hall's Credits tab; and the line *"I agree to the contributor terms in LICENSE.md"*. No GitHub account at all? The desk in the hall's ADD YOUR LEVEL room has a form — send a link to the files from there.

What happens next: Lightsmith Forge looks at every submission, may ask for changes on the pull request, and merges the good ones. A merged level or game goes live at lightsmithforge.linkpc.net/hub/ and in this copy — and so on itch.io and Game Jolt, which show this copy. The credit goes on the hall's Credits tab.

## The rules, short

- Change only the COMMUNITY block of `index.html` and your own `community/<slug>/` folder.
- Your own work, or assets whose licence allows it (CC0; CC BY with the credit; bought assets only where their licence allows redistribution) — list every one.
- Nothing that phones home: no trackers, no ads, no logins, no hidden network calls.
- Keep the hall fast: no THREE lights, small files, few draw calls.
- Leave the licence notice and the credits as they are.

## Terms

The hall is © Lightsmith Forge — source-available, all rights reserved (`LICENSE.md`). Copying and changing it is allowed for one purpose: building a level or a game to submit here, the way this page describes — including running your copy and publishing it from your fork while you build, and using a coding assistant on it. By submitting you confirm that the work is yours, or that every part of it carries a licence that allows it, and you grant Lightsmith Forge a perpetual, worldwide, royalty-free, non-exclusive licence to use, adapt, show and distribute it as part of The Arrivals Hall on every copy of the hall. You keep the copyright of your own work and stay free to use it elsewhere. Lightsmith Forge decides what is hung, and may edit or take down a contribution. The full wording is in `LICENSE.md`, section *Contributing a level or a game*.
