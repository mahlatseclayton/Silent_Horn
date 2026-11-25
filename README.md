# The Silent Horn

A 3D story game that runs in the browser, built with [three.js](https://threejs.org/) and [Vite](https://vite.dev/) for the COMS3006A (Computer Graphics and Visualisation) group project.

> When the horn leaves the stone, the forest falls silent. Someone has been paid to take it.

- Repository: https://github.com/motshekhene/cgv-project
- Local development server: http://localhost:5173/ (after `npm run dev`)

---

## Contents

1. [The game](#1-the-game)
2. [Getting started](#2-getting-started)
3. [Running, building and deploying](#3-running-building-and-deploying)
4. [Controls](#4-controls)
5. [Project structure](#5-project-structure)
6. [How the code fits together](#6-how-the-code-fits-together)
7. [Graphics and shaders](#7-graphics-and-shaders)
8. [Assets and credits](#8-assets-and-credits)
9. [Team rules](#9-team-rules)
10. [Performance targets](#10-performance-targets)
11. [Further documentation](#11-further-documentation)
12. [Team](#12-team)

---

## 1. The game

Kai is a young forest guide. An old horn lies on a stone up the ridge, and the valley's story says that if the horn ever leaves the stone, the whole forest goes silent. A logging company wants the forest cleared, but its men will not go past the stone. Baba Zwane, the old guide who raised Kai on stories by the fire, sends him up the ridge for the horn. From the moment he lifts it, the company's Marshal hunts him on foot, by car and finally face to face at the falls.

The game is played in one continuous run, each chapter handing straight to the next:

```
title -> prologue -> level01 -> level02-intro -> level02 -> level03 -> epilogue
```

| Chapter | Name | What you do |
|---|---|---|
| Title | The glade at dawn | The main menu, drawn over a live 3D scene of the horn on its stone. Choose your player, change options, browse cards, records and credits. |
| Prologue | The Fire and the Stone | Walk the valley at night, hear Baba Zwane's story at the fire, then climb to the stone and take the horn (or refuse it). |
| Level 1 | The Old Trail | A three-lane chase run through jungle ruins. Jump, slide and steer around logs, arches and rocks while the Marshal closes in behind. Catch Forest Lights to fill the horn, then blow it to clear the trail ahead and trip him with roots. Ends with Kai reaching the car at the bay. |
| Level 2 intro | The drive-out | A cutscene: Kai takes the car out of the jungle onto the River Road. |
| Level 2 | The River Road | A driving chase about 4 km long on a mud road beside the river, from sunset into night and rain. Dodge fallen trees, rockfalls and crossing animals while the Marshal's car and drones attack. Forest Lights buy new cars in the car yard. Ends with the car going over the waterfall. |
| Level 3 | The Falls | A third-person boss fight in the shrine courtyard below the falls. Fight the Marshal's men, then the Marshal himself through four phases, with a reveal when his mask comes off. Spirit shrines in the jungle ring heal you or give you gifts. A perfect dodge slows time. |
| Epilogue | The Stone | A cutscene: Kai returns the horn to its stone and the forest wakes again. |

### Features beyond the main story

- **Player select.** Play as Kai, Naledi, Bheki or Knox. Every character has the full move set and the story text adjusts to their name and pronouns (`src/player/roster.js`).
- **Spirit cards.** One collectible card is hidden somewhere in the game each day. Where it hides is given only as an in-game clue; the in-game map shows the landmarks. Found cards are kept in the browser (`src/cards/`).
- **Forest Lights.** The currency caught in Level 1, used to fill the horn and to buy cars in Level 2. It is saved between runs (`src/core/wallet.js`).
- **Records.** Each level keeps its best times and scores, and the end card shows NEW BEST when one is beaten (`src/core/records.js`).
- **Continue.** The main menu remembers the last chapter reached (`src/core/progress.js`).
- **Playbook.** An in-game guide with a page per chapter, the things you will find and the places you will visit (`src/ui/Playbook.js`).
- **Options.** Master and music volume, mouse sensitivity, invert Y, graphics quality (LOW, MEDIUM, HIGH) and an FPS counter, all saved in the browser (`src/core/settings.js`).
- **Original score.** The music for every chapter is synthesised in code with the Web Audio API (`src/audio/`).

---

## 2. Getting started

### Requirements

- [Node.js](https://nodejs.org/) 20.19 or newer (or 22.12 or newer). Vite 8 will not run on older versions.
- npm (comes with Node.js).
- A desktop browser with WebGL 2: a recent Chrome, Edge or Firefox.
- [Git](https://git-scm.com/).

### First-time setup

Anyone added as a collaborator on GitHub can clone the shared repository directly:

```bash
git clone https://github.com/motshekhene/cgv-project.git
cd cgv-project
npm install
npm run dev
```

Then open http://localhost:5173/ in your browser. The game opens on its title screen.

If something breaks after pulling new changes from the team, run `npm install` again first: someone may have added or updated a dependency.

### Dependencies

| Package | Version | Purpose |
|---|---|---|
| [three](https://www.npmjs.com/package/three) | 0.185.1 | The 3D engine (rendering, loaders, animation) |
| [vite](https://www.npmjs.com/package/vite) | 8.2.0 | Development server and production build |

There is no other runtime dependency. Physics, AI, audio and UI are all written in the project itself.

---

## 3. Running, building and deploying

### npm scripts

| Command | What it does |
|---|---|
| `npm run dev` | Starts the Vite development server at http://localhost:5173/ with hot reload. |
| `npm run intro:l2` | Starts the server and opens the Level 2 drive-out cutscene on its own page. |
| `npm run build` | Builds the game for production into `dist/`, and copies the `assets/` folder into `dist/assets/`. |
| `npm run preview` | Serves the built `dist/` folder locally, to check a production build before uploading it. |

### Jumping to a chapter

Add `?level=<name>` to the URL to open any chapter directly. This is useful while developing:

| Chapter | URL |
|---|---|
| Title screen | http://localhost:5173/ |
| Prologue | http://localhost:5173/?level=prologue |
| Level 1 | http://localhost:5173/?level=level01 |
| Level 2 drive-out | http://localhost:5173/?level=level02-intro |
| Level 2 | http://localhost:5173/?level=level02 |
| Level 3 | http://localhost:5173/?level=level03 |
| Epilogue | http://localhost:5173/?level=epilogue |

The chapter names are registered in `src/main.js`. While the game is running, `window.game` is available in the browser console for debugging.

### Cutscene pages

The Level 2 drive-out can also be opened on its own page: http://localhost:5173/intros/level2-intro.html

That page accepts two extra parameters:

- `?t=6.5` starts the scene 6.5 seconds in.
- `?hold=7` stops the clock at 7 seconds, to inspect a single frame.

R replays the scene, Space, Enter or a click skips to the end, and Esc pauses.

### Tools pages

- http://localhost:5173/tools/build-player.html builds a new playable character in the browser from any Mixamo FBX (see [section 6](#adding-a-new-player-character)).
- http://localhost:5173/tools/concepts/ holds the concept renders used during planning (reference only).

### Deploying

The game is hosted inside a subfolder of a LAMP web server, not at the root of the site. `vite.config.js` sets `base: './'` so every URL in the build is relative, which is why the [path rule](#91-file-paths-must-start-with--never-) below matters.

To deploy:

1. Run `npm run build`.
2. Upload the whole contents of `dist/` to the game's folder on the server.
3. Open that folder's URL in a browser and play through once to confirm every model, texture and sound loads (check the browser's Network tab for any 404s).

`dist/` is ignored by Git. Always build it fresh before uploading.

---

## 4. Controls

The pause menu (Esc) lists the controls for the chapter being played, and CONTROLS on the main menu lists them for every chapter. Keys are read from the live bindings in `src/core/Input.js`.

### Every chapter

| Action | Keys |
|---|---|
| Pause | Esc |
| Mute | M |
| Skip a line, card or cutscene | Space, Enter or left click |

### Main menu

| Action | Keys |
|---|---|
| Choose | Up / Down or W / S |
| Select | Enter or click |
| Back | Esc |

### Prologue

| Action | Keys |
|---|---|
| Look | Mouse |
| Walk | W A S D |
| Use, confirm | E |
| Leave the horn (twice to walk away) | Q |
| Map (bigger or smaller) | N |
| Skip the intro | X |

### Level 1: The Old Trail

| Action | Keys |
|---|---|
| Steer between lanes | A / D or Left / Right |
| Jump | Space, Up or W |
| Slide | Ctrl, Down or S |
| Boost | Shift |
| Look back | Right mouse button or C |
| Blow the horn (when full) | V or Q |
| Restart | R |

### Level 2: The River Road

| Action | Keys |
|---|---|
| Drive / reverse | W / S |
| Steer | A / D or Left / Right |
| Drift (hold while steering) | Q |
| Handbrake | Space |
| Boost | Shift |
| Blow the horn (when ready) | F |
| Open the car yard | V |
| Change paint in the car picker | Q / E |
| Switch camera (chase view or driver's seat) | C |
| Music on / off | N |

### Level 3: The Falls

| Action | Keys |
|---|---|
| Look | Mouse |
| Move | W A S D |
| Punch | Enter or left mouse button |
| Kick | K |
| Block (hold), parry (tap just before a hit) | B or right mouse button |
| Dodge | C |
| The horn: slow time | V or Q |
| Lock on | Tab |
| Map (bigger or smaller) | N |
| Restart | R |

Strings of punches, kicks and dodges become special moves:

| Trick | Input |
|---|---|
| One-two kick | Punch, punch, kick |
| Switch hook | Kick, kick, punch |
| Whirlwind | Punch, kick, punch, kick |
| Slip counter | Dodge, punch |
| Snap kick | Dodge, kick |

On touch screens, Level 3 shows on-screen buttons (`src/ui/TouchControls.js`).

---

## 5. Project structure

```
cgv-project/
├── index.html                 The game page. Loads src/main.js.
├── package.json               npm scripts and the two dependencies (three, vite).
├── vite.config.js             Relative base path ('./') and the step that copies assets/ into dist/.
├── README.md                  This file.
│
├── src/                       All game code (plain JavaScript ES modules).
│   ├── main.js                Entry point. Registers every chapter, wires the menus, starts the game.
│   ├── style.css              Page-level styles.
│   │
│   ├── core/                  The engine layer shared by every chapter.
│   │   ├── Game.js            Owns the renderer, camera, frame loop, level switching and quality settings.
│   │   ├── Level.js           Base class every chapter extends (init, update, teardown) and disposeObject().
│   │   ├── GameState.js       The one shared state object (health, stamina, distance, letters, ...).
│   │   ├── Input.js           Keyboard and mouse input, with named action bindings.
│   │   ├── AssetRegistry.js   Loads and caches models, textures and audio; enforces the './' path rule.
│   │   ├── PostFX.js          HDR post-processing: bloom, god rays, colour grade, vignette, grain.
│   │   ├── settings.js        Player options saved in the browser.
│   │   ├── progress.js        Last chapter reached, for CONTINUE.
│   │   ├── records.js         Best times and scores per level.
│   │   └── wallet.js          Forest Lights, the in-game currency.
│   │
│   ├── levels/                The chapters.
│   │   ├── TitleScene.js      The 3D glade behind the main menu.
│   │   ├── Prologue.js        The fire, Baba Zwane's story and the horn on the stone.
│   │   ├── Level01.js         Level 1: the chase run on the Old Trail.
│   │   ├── Level02.js         Level 2: the driving chase on the River Road.
│   │   ├── Level03.js         Level 3: the boss fight at the Falls.
│   │   ├── Epilogue.js        The horn returned to its stone.
│   │   ├── jungle/            Shared jungle helpers: props, palette, sky.
│   │   ├── prologue/          Prologue landmarks and walking paths.
│   │   ├── level1/            Jungle world builder, horn call, car door, light pool.
│   │   ├── level2/            Vehicle controller, Marshal AI and weapons, road, traffic, course,
│   │   │                      obstacles, pickups, car select and paint, damage, rain, river, HUD, sound.
│   │   └── level3/            Combat controller, boss, enforcers, shadow stag, arena, navigation,
│   │                          telegraphs, storm, wetness, style meter, awards, IK and foot planting.
│   │
│   ├── intros/                Cutscene framework and the cast.
│   │   ├── Cutscene.js        Base class for scripted scenes (timeline driven, skippable).
│   │   ├── cast.js            Builds Kai, the Marshal and the horn for any scene.
│   │   ├── run.js             Runs one cutscene on its own page (used by intros/*.html).
│   │   ├── fx.js              Small shared effects for cutscenes.
│   │   └── level2/            DriveOutIntro.js, the drive-out scene before Level 2.
│   │
│   ├── player/                Playable characters.
│   │   ├── roster.js          The four players, their names and pronouns, and the saved choice.
│   │   └── rig.js             Loads a character's model and animations (with a fallback).
│   │
│   ├── shaders/               Custom GLSL shaders.
│   │   ├── water.js           River and pool water: noise normals, reflection, refraction, Fresnel.
│   │   ├── waterfall.js       The falls.
│   │   ├── lightshaft.js      Light shafts through the canopy.
│   │   ├── wind.js            Vertex wind on trees, bushes and grass.
│   │   ├── rain.js            Level 2 rain.
│   │   ├── jungleSpeedWarpShader.js   Level 1 speed warp at the screen edges.
│   │   ├── noise.js           Shared value noise and fBm.
│   │   └── display.js         Inverse tone mapping so the sky and fog keep their colours under PostFX.
│   │
│   ├── fx/                    Particles (dust, sparks) and the torn-page letters.
│   ├── audio/                 Synthesised music and sound, master volume and mute.
│   ├── cards/                 Spirit cards: the card set, daily hiding spot, pickups, clue signs, art.
│   └── ui/                    Menus and HUDs: title screen, pause, options, controls, credits,
│                              playbook, card album, map, records, loading screen, end cards, fight HUD,
│                              dialogue, FPS counter, touch controls, theme and branding.
│
├── assets/                    Models and textures loaded at runtime (copied into dist/assets/ on build).
│   ├── characters/            Mixamo player and Marshal builds (.glb with a .json of measurements);
│   │                          kai.fbx and handler.fbx are fallbacks if a build fails to load.
│   └── jungle/                Every jungle model and texture, with its own index: assets/jungle/README.md
│       ├── models/nature/     Trees, bushes, grass, rocks (FBX).
│       ├── models/ruins/      Stone shrine pieces with leaf and bark textures (FBX).
│       ├── models/props/      Logs, crates, barrels, boulders, small trees (glTF).
│       ├── models/wreck/      The car wreck in the pool below the falls (GLB).
│       └── textures/          PBR texture sets: colour, normal, roughness, ambient occlusion.
│
├── public/                    Served as-is at the site root (copied into dist/ by Vite).
│   ├── favicon.svg
│   └── assets/
│       ├── audio/             Recorded music and sound effects (see CREDITS.md there).
│       ├── guide/             Screenshots used by the Playbook.
│       ├── level2/            Cars, traffic, animals, the Marshal's car and drone (see CREDITS.md there).
│       └── prologue/          The ruined hut (see CREDITS.md there).
│
├── intros/
│   └── level2-intro.html      The Level 2 drive-out on its own page (npm run intro:l2).
│
├── tools/                     Build tools for the team (not part of the game).
│   ├── build-character.py     Blender script: Mixamo downloads -> character .glb + .json.
│   ├── build-player.html/.js  In-browser tool: any Mixamo FBX -> a new playable character.
│   ├── probe-audio.mjs        Reads an mp3's length and bitrate before it is added to the game.
│   └── concepts/              Scripts that rendered the planning concept images (reference only).
│
└── docs/                      Design documents, plans and the original pitch (see section 11).
```

Folders that exist locally but are **not** committed:

| Folder | Why it is ignored |
|---|---|
| `node_modules/` | Installed by `npm install`. |
| `dist/` | Built by `npm run build`. |
| `_source/` | Raw source packs (`.blend` files, 4K originals, zips). Keep these on the team's shared drive. |
| `new_characters/` | Raw Mixamo FBX downloads (over 100 MB). The game-ready builds live in `assets/characters/`. |
| `tools/concepts/out/` | Concept render output. |

---

## 6. How the code fits together

### The game loop

`src/main.js` creates one `Game` (`src/core/Game.js`) and registers each chapter by name with a factory function:

```js
game.registerLevel("level01", () => new Level01());
await game.setLevel("level01");
```

`Game` owns the WebGL renderer, the main camera, the frame timing and the current level. Every frame it calls the level's `update(dt, state)` and then renders through `PostFX`. When the level changes, the old level is torn down before the new one is built, so nothing leaks between chapters. `game.restart()` rebuilds the current level without reloading the page.

### The level contract

Every chapter, including the title screen and the cutscenes, extends `Level` (`src/core/Level.js`):

| Method | Purpose |
|---|---|
| `init(scene, assets, input, state)` | Build the world. |
| `update(dt, state)` | Advance one frame. |
| `teardown()` | Free everything on the GPU. |

Two rules keep this working:

1. **Everything a level creates goes inside `this.root`.** Teardown is then one call, and memory stays flat across a full playthrough.
2. **Only the shared `GameState` field names are written** (`health`, `stamina`, `boostHeat`, `distance`, `letters`, `handlerState`, `handlerHelmetOff`). The HUDs read these names and nothing else.

### Loading assets

All models, textures and sounds load through `AssetRegistry` (`src/core/AssetRegistry.js`), which is available to every level as `assets`:

```js
const tree = await assets.fbx('jungle/models/nature/tree-1.fbx');
const logs = await assets.model('jungle/models/props/logs.gltf');
const mud  = await assets.texture('jungle/textures/mud-color.jpg', { repeat: [4, 40] });
```

Everything is cached, so asking twice never downloads twice, and the registry throws in development if a path starts with `/` (see [section 9](#9-team-rules)).

### Characters

The player and the Marshal are Mixamo characters built into `.glb` files with every animation as a named clip, plus a `.json` file of measurements (clip lengths, when each hit lands, hip height). Load them with:

```js
import { loadPlayer } from './player/roster.js';       // whoever the player chose
import { loadRig } from './player/rig.js';
const kai = await loadRig(assets, 'kai-bryce', 'kai.fbx');   // a specific rig, with its fallback
```

For cutscenes, `loadCast`, `makeKai` and `makeHandler` in `src/intros/cast.js` build the same characters ready to pose.

#### Adding a new player character

1. Download the character from [Mixamo](https://www.mixamo.com/) with skin, in T-pose, as **FBX Binary**.
2. Run `npm run dev` and open http://localhost:5173/tools/build-player.html.
3. Pick the FBX and give it an id. The tool retargets all of Kai's animations onto it and returns a `.glb` and a `.json`.
4. Save both files into `assets/characters/`.
5. Add a row to `PLAYERS` in `src/player/roster.js` with its name, rig id, a one-line description and its pronouns.

### Win and lose screens

Every level ends on the same card style from `src/ui/theme.js`. A level without a FightHUD or StoryOverlay uses:

```js
import { showEndCard } from './ui/EndCard.js';
showEndCard({ kind: 'win', title, sub, lines, action });   // kind is 'win' or 'lose'
```

---

## 7. Graphics and shaders

The full explanation of each effect, written for the demo, is in [docs/GRAPHICS_AND_SHADERS.md](docs/GRAPHICS_AND_SHADERS.md). In summary:

| Effect | Where | How it works |
|---|---|---|
| HDR rendering and antialiasing | `src/core/PostFX.js` | The scene renders into a half-float target (multisampled on HIGH), so bright values above 1.0 survive for bloom. |
| Bloom | `src/core/PostFX.js` | Bright pass with a soft knee, a 13-tap downsample chain, then a tent-filter upsample added back up. |
| God rays | `src/core/PostFX.js` | Screen-space light scattering: each pixel marches toward the sun and sums the bright sky it passes. |
| Colour grade and lens | `src/core/PostFX.js` | ACES tone mapping, per-level grade, vignette, chromatic aberration, film grain and dither. |
| Damage and impact feedback | `src/core/PostFX.js` | Uniforms driven by game state: a red edge pulse when health drops, a lens kick and flash on impacts. |
| Wind | `src/shaders/wind.js` | Vertex shader injected into the standard material: bend grows with height, each plant has its own phase. |
| Water | `src/shaders/water.js` | Normals from scrolling noise height fields; cube-map reflection and refraction mixed by a Fresnel term. |
| Waterfall, light shafts, rain, speed warp | `src/shaders/` | Custom vertex and fragment shaders animated by time and game state. |
| Particles | `src/fx/Particles.js` | A pooled `THREE.Points` system with a custom shader; noise-broken edges make dust read as a puff. |
| Keeping the original look | `src/shaders/display.js` | Inverse ACES and sRGB so the sky shader and fog look the same with or without post-processing. |

**Graphics quality.** LOW draws straight to the screen with no post-processing. MEDIUM drops MSAA, uses fewer bloom levels and draws god rays at quarter resolution. HIGH turns everything on. Integrated GPUs start on MEDIUM, and if the game runs under 35 FPS for four seconds it steps down one level for that session.

---

## 8. Assets and credits

Every asset the team did not make is credited in the game (CREDITS on the main menu, from `src/ui/credits.js`) and in a credits file next to the asset. When you add an asset, add a row to both.

Per-folder lists:

- [assets/jungle/README.md](assets/jungle/README.md): jungle models and textures, with scale factors and material notes.
- [public/assets/level2/CREDITS.md](public/assets/level2/CREDITS.md): cars, traffic, animals, the Marshal's car and drone.
- [public/assets/audio/CREDITS.md](public/assets/audio/CREDITS.md): recorded music and sound effects.
- [public/assets/prologue/CREDITS.md](public/assets/prologue/CREDITS.md): the ruined hut.

### The forest and the shrine

| Asset | Author | Licence | Link |
|---|---|---|---|
| Simple Nature Pack | Quaternius | CC0 | https://quaternius.com/packs/simplenature.html |
| Ultimate Modular Ruins Pack | Quaternius | CC0 | https://quaternius.com/packs/ultimatemodularruins.html |
| Ultimate Fantasy RTS | Quaternius | CC0 | https://quaternius.com/packs/ultimatefantasyrts.html |
| Universal Base Characters (fallback characters) | Quaternius | CC0 | https://quaternius.com/packs/universalbasecharacters.html |
| Ground 040 (forest floor) | ambientCG | CC0 | https://ambientcg.com/view?id=Ground040 |
| Ground 051 (mud) | ambientCG | CC0 | https://ambientcg.com/view?id=Ground051 |
| Rock 063 (mossy stone) | ambientCG | CC0 | https://ambientcg.com/view?id=Rock063 |
| Car Kit (the wreck) | Kenney | CC0 | https://kenney.nl/assets/car-kit |
| Steering wheel | Poly by Google | CC BY 3.0 | https://poly.pizza/m/bIYbhKwE4L0 |
| Hut | Jarlan Perez | CC BY 3.0 | https://poly.pizza/m/3OlnbRfwPLc |

### The River Road

| Asset | Author | Licence | Link |
|---|---|---|---|
| Cars Bundle (Street Racer and traffic) | Quaternius | CC0 | https://poly.pizza/bundle/Cars-Bundle-FE5IWe6OMk |
| Toyota AE86 (the Drifter) | IvOfficial | CC BY 3.0 | https://poly.pizza/m/ZEFWmOPSgh |
| Car (the Muscle) | theking1322 | CC BY 3.0 | https://poly.pizza/m/t8njpnyrxg |
| Convertible (the Executive) | Poly by Google | CC BY 3.0 | https://poly.pizza/m/dggOiBLYyuR |
| CAR Model (the Supercar) | Ignition Labs | CC BY 3.0 | https://poly.pizza/m/5zUWP5UsLg- |
| Range Rover (the Marshal's car) | IvOfficial | CC BY 3.0 | https://poly.pizza/m/8zk4o6nALW |
| Richie (the Marshal's drones) | joney_lol | CC BY 3.0 | https://poly.pizza/m/BwaLw2Olre |
| Pickup Truck (the Bruiser and traffic) | Quaternius | CC0 | https://poly.pizza/m/qn4grQgHm8 |
| Van (traffic) | jeremy | CC BY 3.0 | https://poly.pizza/m/9hUUD2DWk1v |
| Bus (traffic) | Poly by Google | CC BY 3.0 | https://poly.pizza/m/4CPpvEmrMoF |

### Animals

| Asset | Author | Licence | Link |
|---|---|---|---|
| Boar (the warthogs) | Poly by Google | CC BY 3.0 | https://poly.pizza/m/57fSWum6F1P |
| Stag (the kudu) | Quaternius | CC0 | https://poly.pizza/m/tQdzbZ1Cmw |
| Deer (the kudu) | Quaternius | CC0 | https://poly.pizza/m/T6Cs7tmMHJ |

### Characters and animation

| Asset | Author | Licence | Link |
|---|---|---|---|
| Characters and animations | Mixamo (Adobe) | Royalty-free | https://www.mixamo.com/ |

### Recorded music and sound

The score is written in code, and every other sound is synthesised with the Web Audio API, except these:

| Asset | Author | Licence | Link |
|---|---|---|---|
| Repeat (title screen music) | SoundUniverseStudio | Pixabay | https://pixabay.com/music/video-games-repeat-gaming-background-music-instrumental-218942/ |
| Collect Points | Liecio | Pixabay | https://pixabay.com/sound-effects/collect-points-190037/ |
| Car crash (swerving, and crash) | RSF_STUDIOS | Pixabay | https://pixabay.com/sound-effects/car-crash-swerving-and-crash-592672/ |
| Racing car engine sound loops | domasx2 | CC0 | https://opengameart.org/content/racing-car-engine-sound-loops |
| Big Explosion | elnineo | CC0 | https://opengameart.org/content/explosion-tilesets |

### Techniques the shader code follows

The shader code is the team's own; these are the published methods it is based on.

| Technique | Source | Link |
|---|---|---|
| Bloom (13-tap downsample, tent upsample) | Jorge Jimenez, SIGGRAPH 2014 | https://www.iryoku.com/next-generation-post-processing-in-call-of-duty-advanced-warfare/ |
| God rays | Kenny Mitchell, GPU Gems 3 chapter 13 | https://developer.nvidia.com/gpugems/gpugems3/part-ii-light-and-shadows/chapter-13-volumetric-light-scattering-post-process |
| Value noise and fBm | The Book of Shaders, Patricio Gonzalez Vivo and Jen Lowe | https://thebookofshaders.com/13/ |
| ACES filmic tone curve | Stephen Hill, via three.js (MIT) | https://threejs.org/ |

### Type and code

| Item | Author | Licence | Link |
|---|---|---|---|
| Crimson Pro (font) | Jacques Le Bailly | SIL OFL 1.1 | https://fonts.google.com/specimen/Crimson+Pro |
| three.js | three.js authors | MIT | https://threejs.org/ |
| Vite | Vite authors | MIT | https://vite.dev/ |

### Licence links

- CC0: https://creativecommons.org/publicdomain/zero/1.0/
- CC BY 3.0: https://creativecommons.org/licenses/by/3.0/
- Pixabay licence: https://pixabay.com/service/license-summary/
- SIL Open Font Licence 1.1: https://openfontlicense.org/
- MIT: https://opensource.org/license/mit

---

## 9. Team rules

### 9.1 File paths must start with `./`, never `/`

Anywhere you load a model, texture, sound or other file, the path must start with `./` (or `../` for a folder up). Never start it with a plain `/`.

Wrong (breaks once hosted):

```js
loader.load('/assets/models/spaceship.glb', ...);
const texture = textureLoader.load('/assets/textures/rock.jpg');
```

Correct:

```js
loader.load('./assets/models/spaceship.glb', ...);
const texture = textureLoader.load('./assets/textures/rock.jpg');
```

The same applies in HTML:

```html
<script type="module" src="./src/main.js"></script>
```

**Why:** the game is not hosted at the top of the website but inside a folder. A path starting with `/` skips past that folder and points to the wrong place. It works on your own laptop, then breaks as soon as it is uploaded, so the bug is easy to miss until it is too late. `AssetRegistry` throws during development if you pass a path starting with `/`, to catch this early.

### 9.2 Filenames: lowercase, no spaces

Use `rock-texture.png`, not `Rock Texture.PNG`. The web server is case-sensitive. Windows and macOS are not, so this bug hides during development and only appears once hosted.

### 9.3 Models and textures

- Load them through `AssetRegistry` (`assets.model(...)`, `assets.fbx(...)`, `assets.texture(...)`), not your own loader, so they are cached and freed between levels.
- Reuse the shared models in `assets/characters/` and `assets/jungle/` rather than adding copies.
- A model only one level needs goes in that level's own folder, for example `public/assets/level2/`.
- Prefer `.glb`, keep textures at 2K or smaller, and credit where it came from (see [section 8](#8-assets-and-credits)).

### 9.4 Win and defeat screens

Use the shared end card (`showEndCard` from `src/ui/EndCard.js`) so every level ends the same way.

### 9.5 Commit and push often to your own branch

Small, frequent commits are better than large changes left unpushed for days.

### 9.6 When in doubt, ask before pushing to `main`

If you are not sure whether something will break the project for everyone, check with the group first.

---

## 10. Performance targets

Measured on a mid-range laptop:

- **Frame rate:** 60 FPS in normal play, and never below 30 FPS with the chase, traffic and shadow-casting headlights all active. Measure with the browser DevTools Performance tab, or turn on the FPS counter in OPTIONS.
- **Draw calls:** keep each scene under about 300 (`renderer.info.render.calls`). Shared models are cached in `AssetRegistry` and cloned with `SkeletonUtils.clone`, so repeated vehicles share one set of geometry and materials.
- **Memory:** nothing is created or destroyed during play. Vehicles, skid marks, smoke and particles use fixed pools recycled every frame. `Level.teardown()` and `AssetRegistry.dispose()` free GPU resources on every level change, including animated models' bone textures. Check for leaks with DevTools Memory heap snapshots before and after a long session.
- **Loading:** every asset loads once and is cached, so a restart or a car swap never downloads again. Level 1's models load in the background while the prologue plays, so the hand-off is instant. Verify on the Network tab.

---

## 11. Further documentation

| Document | What it covers |
|---|---|
| [docs/GRAPHICS_AND_SHADERS.md](docs/GRAPHICS_AND_SHADERS.md) | Every graphics effect and shader, how it works, and how it maps to the marking rubric. |
| [docs/JUNGLE_SHRINE_IMPLEMENTATION.md](docs/JUNGLE_SHRINE_IMPLEMENTATION.md) | The original implementation guide for the Jungle Shrine theme: beats, layout, look and asset use per level. |
| [docs/LEVEL1B_JUNGLE_SHRINE.md](docs/LEVEL1B_JUNGLE_SHRINE.md) | Level 1 world and environment notes. |
| [docs/LEVEL1_2_INTROS_AND_WINS.md](docs/LEVEL1_2_INTROS_AND_WINS.md) | The Level 1 and Level 2 intro and win scenes. |
| [docs/LEVEL3_THEME_REDESIGN.md](docs/LEVEL3_THEME_REDESIGN.md) | The Level 3 redesign for the Jungle Shrine theme. |
| [docs/LEVEL3_ASSET_PLAN.md](docs/LEVEL3_ASSET_PLAN.md) | Assets planned for Level 3. |
| [docs/CAR_SEAT_AND_PLAYER_SELECT_PLAN.md](docs/CAR_SEAT_AND_PLAYER_SELECT_PLAN.md) | Player select and seating each player in the cars. |
| [docs/blackout-protocol-pitch.pdf](docs/blackout-protocol-pitch.pdf) | The original game pitch. |
| [docs/team-task-separation.pdf](docs/team-task-separation.pdf) | How the work was split across the team. |
| [docs/Meeting-Improvements-2026-10-07.pdf](docs/Meeting-Improvements-2026-10-07.pdf) | Improvements agreed at the 7 October 2026 meeting. |
| [docs/game-ideas.tex](docs/game-ideas.tex) | Early game ideas. |
| [docs/concepts/](docs/concepts/) | Concept pages and storyboards from planning (some for earlier themes). |
| [assets/jungle/README.md](assets/jungle/README.md) | Index of every jungle model and texture, with scale factors. |

Some planning documents describe earlier versions of the story (a data-centre prologue and a "BLACKOUT" key). The code and this README describe the game as it is now.

---

## 12. Team

| Member |
|---|
| Sebetola Junior (project manager) |
| Maredi Mahlatse |
| Mbatha Nontokozo |
| Monaiwa Realeboha |
| Modiakgotla Keamogetswe |
| Nkadimeng Kgothatso |

Questions: ask in the group chat or ask the PM (Junior). Do not stay stuck for too long.
