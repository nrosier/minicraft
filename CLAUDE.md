# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project scope

Minicraft is a lightweight 3D voxel game that runs entirely in the browser (HTML5 canvas + Three.js). There is no backend and no build step: open `index.html` (ideally via any static server, e.g. `python3 -m http.server`) to run it. Three.js is loaded from the jsDelivr CDN through an import map, pinned to an exact version. The whole game lives in `index.html`.

## Commands

- Run: `python3 -m http.server 8000`, then open http://localhost:8000 (ES module imports may not work from `file://` in all browsers).
- There is no build, lint, or test tooling. Do not add build dependencies for the base game.

## Architecture

Detailed architecture (world, generation, rendering, player, mining, animals, controls, save format) is in the `minecraft` skill (`.claude/skills/minecraft/SKILL.md`). Load it before changing gameplay, world, rendering, animals, controls, or persistence.

## Code standards

- Keep the game runnable with zero build dependencies (single HTML file or plain ES modules).
- Performance: never create one mesh per block; keep merged geometry and face culling.
- If you change the save format, bump `version` and keep validating on load.
- W/A/S/D are physical key codes (`e.code`), so they are Z/Q/S/D on AZERTY — don't switch to `e.key`.
