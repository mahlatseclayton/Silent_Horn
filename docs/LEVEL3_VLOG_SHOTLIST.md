# Level 3 vlog: shot list

What to have on screen for each part of the voice-over (`docs/LEVEL3_VLOG_VOICEOVER.md`), and the shader files to record. Paths are from the project root (`cgv-project/`).

## What to show, in order

1. **Opening:** start on Kai lying in the pool next to his broken car, then him getting up and shaking off the water.
2. **The Marshal arrives:** the rope slide, the jump off the arch, his men following, the face-to-face talk, the VS screen.
3. **Attempt 1:** the three men, then the Marshal, his attacks lighting up on the ground, Kai's health running out, the *DEFEATED* card.
4. **Shaders:** the two code screenshots below, then the GitHub repo (https://github.com/motshekhene/cgv-project) showing the Level 3 shader files as you name them.
5. **Attempt 2:** press **R**, the men coming down the rope. Point at or zoom into each part of the screen as you name it: Kai's box, the enemy health bar, the camera button, the map, the buttons, the off-screen arrow and shrine markers.
6. **Spirit shrines:** Kai stepping onto a stone circle, the spirit jumping into him, the glowing hands, the attack names under the health bar.
7. **Beating the Marshal:** the mask coming off, then phase three (sunset, torches, rain, red water), then phase four (he takes the horn, the blast ring, the lightning hitting him), then the slow-motion last hit.
8. **The kudu:** the horn glowing red, the stone stag breaking open and jumping down, Kai losing to it, the *DEFEATED* card.
9. **Attempt 3:** **R** again, the style meter, damage numbers, words on screen, beating the Marshal, the stag coming down.
10. **Beating the kudu:** pressing **V** (grey screen, blue horn), the stag charging into a tree, "STUCK — STRIKE!", **E** onto its back, the stag turning to stone, "THE HORN IS CLEAN".
11. **After the fight:** fireflies, Kai picking up the horn, the last words, Kai blowing the horn, the *VICTORY* card.
12. **Epilogue:** press CONTINUE: the quiet forest, the horn put back on its stone, the ring of light, birds flying up, *THE END*.

## The two shaders you explain (after defeat 1)

Open each file in the editor at these lines, then screenshot or screen-record it.

| # | File to record | Lines | Highlight | Gameplay to show with it |
|---|---|---|---|---|
| 1 | `src/levels/level3/Telegraphs.js` | 38–64 | 59–60 | The coloured lanes and circles filling before the Marshal's attacks |
| 2 | `src/shaders/water.js` | 52–89 | 67, 74–75 | Low camera across the pool (mirror), then looking down into it |

## The other Level 3 shaders: where they are in the repo

Show these on GitHub while you name them. They're in the same order you say them.

| Shader | File |
|---|---|
| Waterfall | `src/shaders/waterfall.js` |
| The Shadow Stag's glowing cracks | `src/levels/level3/ShadowStag.js` |
| Spirit shrines filling with light | `src/levels/level3/Awards.js` |
| Grey slow-motion screen | `src/levels/level3/KeyVision.js` |
| Light trails behind Kai's kicks | `src/levels/level3/Trails.js` |
| Fireflies | `src/levels/level3/Fireflies.js` |
| Wet footprints | `src/levels/level3/Wetness.js` |
