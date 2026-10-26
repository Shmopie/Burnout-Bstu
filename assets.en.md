# BURNOUT — assets & licenses

**Game:** BURNOUT: You Are the Semester  
**Platform:** web (HTML5 / WebGL)  
**Repository:** source code plus `public/` and `Characters/`

This document is for the jury: which resources we used, under what terms, and what the team made from scratch.

**Russian version:** [assets.md](assets.md)

---

## 1. Made by the team (original work)

Everything below was created by the project team during the game jam (code, data, procedural art). The shipped game does **not** include third-party sprite packs, tilesets, audio libraries, or a commercial game engine.

| Category | Location | Description |
|----------|----------|-------------|
| **Game source code** | `src/` | Logic, UI, AI, camera, modes (story, arcade, bosses, duel), EN/RU localization |
| **Data & balance** | `src/data/` | Semester weeks, cards, dialogue, strings, `balance.json` |
| **Kirill (hero)** | `src/hero/person.ts`, `look.ts`, `kirill.ts` | Procedural low-poly body and pose animation in code; **no separate GLB for Kirill** |
| **Horde units** | `src/horde/unitModels.ts` | All “cards” (pop quiz, deadline, med ball, roach, etc.) built from Three.js primitives in code |
| **Maps & props** | `src/maps/` | Week layouts, pathfinding grid, furniture and décor (`props.ts`), background life |
| **Floor & sign textures** | `src/render/textures.ts` | Drawn on `<canvas>` at runtime (tiles, asphalt, “317”, “Dean’s office”, etc.) |
| **UI icons** | `src/ui/icons.ts` | Hand-drawn SVG paths (coffee, bell, bolt, eye…) — not emoji image files |
| **Shaders & post-processing** | `src/render/toon.ts`, `post.ts`, `fx.ts` | Cel-shading, outlines, bloom, vignette |
| **Music & sound** | `src/core/audio.ts` | **100% Web Audio API synthesis** (oscillators, noise, reverb); **no .mp3/.wav shipped** |
| **Voice (optional)** | `public/voice/` | Hook for custom recordings; repo only has `README.txt`, **no voice files** |
| **Rigging script** | `tools/autorig.py` | Auto skeleton and weights in Blender for T-pose GLB → `public/models/*.glb` |
| **HUD portraits** | `public/portraits/*-face.jpg`, `*-body.jpg` | 2D character portraits for UI; prepared by the team for the cast |
| **Source meshes (T-pose)** | `Characters/*.glb` | Pre-rig sources (same characters as in `public/models/`) |
| **Tests** | `scripts/*-smoke.ts` | Headless checks (not part of the player build) |

**Story, character names, BrSTU locations, and joke lines** are original team writing.

---

## 2. Third-party resources (assets & services)

### 2.1. 3D characters (GLB)

| Files | Source | License / rights |
|-------|--------|------------------|
| `public/models/nina.glb`, `pasha.glb`, `artem.glb`, `shady.glb`, `sonya.glb`, `romchik.glb`, `masha.glb`, `grisha.glb` | Base meshes generated with **[Meshy.ai](https://www.meshy.ai)** (AI 3D), then processed by the team | Rights to generated models under **[Meshy Terms of Service](https://www.meshy.ai/terms)** (team account). After export: scale, **custom rig** (`tools/autorig.py`), in-game optimization |
| `Characters/*.glb` | Same source meshes (T-pose before rigging) | Same as above |

**Note:** GLB files contain **no animation clips** — motion is driven by procedural poses in code (`src/assets.ts`, `src/hero/person.ts`). If a GLB fails to load, the game uses a procedural placeholder in the same toon style.

### 2.2. Fonts (Google Fonts)

Loaded from CDN in `index.html` (internet required on first run):

| Font | Use | License |
|------|-----|---------|
| [Nunito](https://fonts.google.com/specimen/Nunito) | UI, labels | [SIL Open Font License 1.1](https://openfontlicense.org/) |
| [JetBrains Mono](https://fonts.google.com/specimen/JetBrains+Mono) | Monospace UI, code motifs | SIL OFL 1.1 |
| [Russo One](https://fonts.google.com/specimen/Russo+One) | Titles, debt stamp, bosses | SIL OFL 1.1 |
| [Cormorant SC](https://fonts.google.com/specimen/Cormorant+SC) | Arena / spell accents | SIL OFL 1.1 |

### 2.3. Software libraries (dependencies, not media)

Installed as npm packages; Vite bundles them into `dist/`.

| Package | Role | License |
|---------|------|---------|
| [three](https://github.com/mrdoob/three.js) r170 | WebGL, GLB loading | [MIT](https://github.com/mrdoob/three.js/blob/dev/LICENSE) |
| [vite](https://github.com/vitejs/vite) | Build tool and dev server | MIT |
| [typescript](https://www.typescriptlang.org/) | Development language | [Apache-2.0](https://github.com/microsoft/TypeScript/blob/main/LICENSE.txt) |
| happy-dom | Dev tests only | MIT |

Three.js examples used in the project (GLTFLoader, MeshoptDecoder, SkeletonUtils) are part of three.js (MIT).

### 2.4. Tools (not shipped with the game)

| Tool | Purpose |
|------|---------|
| [Blender](https://www.blender.org/) 4.x | Headless rigging via `tools/autorig.py` (GPL tool; **not included in the game**) |
| Node.js | Build and tests |

---

## 3. What we did not use

- Ready-made **music tracks** or **SFX packs** (everything is synthesized in code).
- **Sprite** or **texture packs** from Asset Store, itch.io bundles, etc.
- **Unity / Unreal** assets (the game uses Three.js).
- **Video** or **motion capture** data.
- **Recorded voice files** in the repository (optional slot; see `public/voice/README.txt`).
- **Third-party company logos or trademarks** (the story references the university setting; in-game “BrSTU 60th anniversary” hoodie art is fictional game art).

---

## 4. Emoji in data files

`src/data/cards.ts` stores Unicode symbols (📝, ⏰…) in some `icon` fields. The **running game** replaces them with **custom SVG icons** (`installIcons()` in `src/ui/icons.ts`). Emoji are not loaded as asset files.

---

## 5. Build for verification

```bash
npm install
npm run build    # output in dist/ — what players run
```

`dist/` contains: `index.html`, JS/CSS bundle, `models/`, `portraits/`, `voice/README.txt`.

---

## 6. Contact

Asset rights questions: **[team name / email]**.
