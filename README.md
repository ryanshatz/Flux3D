# Flux3D — Five9 IVR Call-Flow Visualizer

<div align="center">

**An open-source, immersive 3D visualizer for Five9 IVR call flows**

Walk through your IVR logic in a navigable 3D environment — complete with a holographic avatar, animated data cables, real-time analytics, and interactive module inspection.

[🚀 **Live Demo →**](https://ryanshatz.github.io/Flux3D/) · [📦 **Get Started**](#quick-start) · [📖 **Controls**](#controls)

</div>

---

## Overview

Flux3D transforms Five9 IVR (Interactive Voice Response) scripts into interactive 3D environments you can explore. Upload any `.five9ivr` XML file and watch your call-flow logic materialize as a navigable 3D world with flowing data cables, glowing modules, and atmospheric particle effects.

Built for contact center engineers, telecom analysts, and anyone who needs to understand complex IVR routing at a glance.

## Features

### 🎮 3rd-Person Avatar Navigation
- **WASD movement** with smooth acceleration and deceleration — no jarring starts/stops
- **Sprint** — Hold `Shift` to move faster (with subtle camera shake for immersion)
- **Zoom** — Scroll wheel adjusts camera distance and angle
- **Free Camera** — Press `Tab` to toggle orbit/free-look mode
- **Click-to-Walk** — Click any module to auto-navigate the avatar to it
- **Double-Click Fly-to** — Double-click any module to instantly teleport nearby

### 🏗️ Premium Module Geometries
Every IVR module type has a unique, identifiable 3D shape on a glowing platform base with idle floating animation and breathing glow:

| Module Type | 3D Shape | Color |
|---|---|---|
| **IncomingCall** | Torus portal + glowing sphere | Cyan |
| **SkillTransfer / Agent** | Industrial cylinder with flanges | Orange |
| **Case / IfElse** | Diamond octahedron + spinning wireframe | Yellow |
| **Hangup** | Compact box with X cross | Red |
| **Play** | Speaker cone with wave rings | Purple |
| **SetVariable** | Gear torus + center sphere | Steel Blue |
| **BlockedCaller** | Shield with X cross | Pink |
| **CRM / Database** | Stacked disks with connector | Green |

### 🔌 Animated Cable Routing
- **Manhattan routing** — All cables use orthogonal 90° turns with smooth CatmullRom curves
- **Flowing data particles** — Animated glowing particles travel along each cable showing data flow direction
- **Electric pulse waves** — Periodic brightness spikes travel the cable length
- **Breathing glow** — Cable emissive intensity oscillates with a subtle pulse
- **Color-coded connections** — Default (blue), Branch (orange), Hangup (red), Success (green), Error (coral)
- **Heat-map integration** — Cable thickness and particle density scale with call volume

### 📊 Analytics & Diagnostics
- **Heat Map Mode** — Toggle to visualize call volume (thicker cables = more traffic, friction modules glow red)
- **Path Tracing** — Click any module to trace the full upstream + downstream call path (dims unrelated cables)
- **Dead-End Detection** — Automatically logs unreachable or terminal modules
- **Live Stats** — Module count, connection count, blocked ANI count, skill transfer count
- **Module Inspector** — Click any module for detailed properties, TTS text, decision branches, and connection info
- **ANI Expansion** — Expand blocked caller ANI node clusters around case modules

### ✨ Immersive Atmosphere
- Deep navy gradient skybox
- Hex circuit-board ground with animated pulse rings
- **1200+ glow-sprite particles** with additive blending and size variation
- **50 firefly particles** — large, bright, pulsing accents drifting throughout the scene
- Bloom post-processing for glowing emissive modules
- Per-module idle floating and breathing glow — every module gently bobs independently
- Glassmorphism UI panels with backdrop blur

### 🔍 Search & Interaction
- **`Ctrl+F`** — Search modules by name or type with real-time filtering
- **Hover tooltip** — Module name, type, and emoji indicator follow the cursor
- **Smooth hover effects** — Scale and glow lerp smoothly on hover (no instant snapping)
- **`?`** — Toggle keyboard shortcuts overlay
- **Screenshot** — Export branded PNG snapshots of the current view

## Quick Start

### Prerequisites
- [Node.js](https://nodejs.org/) (v18+)
- npm

### Install & Run
```bash
git clone https://github.com/ryanshatz/Flux3D.git
cd Flux3D
npm install
npm run dev
```
Open `http://localhost:5173/Flux3D/` in your browser.

### Load an IVR Script
1. Click **"Load IVR"** in the toolbar
2. Select any `.five9ivr` XML file exported from Five9
3. The 3D scene builds automatically with spring-animated module entrances

A sample IVR script (`INBOUND OPEN.five9ivr`) is included and loads automatically on startup.

### Optional: Heat Map Data
1. Click **"Heat Map CSV"** in the toolbar
2. Upload a CSV call log with columns for module paths and call counts
3. Cable thickness, particle density, and module glow scale with call volume
4. Friction modules glow red, success modules glow green

## Controls

| Key | Action |
|---|---|
| `W` `A` `S` `D` / Arrow Keys | Move (camera-relative) |
| `Shift` | Sprint (with camera shake) |
| `Tab` | Toggle free camera / 3rd person |
| `Scroll` | Zoom in/out |
| `Click` | Select module → inspect + auto-walk + trace path |
| `Double-Click` | Teleport to module |
| `Click Empty Space` | Clear selection and path trace |
| `Ctrl+F` | Search modules |
| `F11` | Toggle fullscreen |
| `?` | Keyboard shortcuts |
| `Right-Drag` | Pan camera (free cam mode) |

## Tech Stack

| Layer | Technology |
|---|---|
| 3D Engine | [Three.js](https://threejs.org/) r172 + EffectComposer (UnrealBloom) |
| Build Tool | [Vite](https://vitejs.dev/) 6 |
| UI | Custom CSS design system (glassmorphism, CSS variables, dark theme) |
| Parser | Custom XML parser for Five9 IVR schema |
| Labels | CSS2DRenderer for always-facing module labels |
| Particles | Custom glow-sprite system with additive blending |

## Project Structure

```
Flux3D/
├── index.html              # Main HTML with toolbar, inspector, overlays
├── vite.config.js          # Vite config (GitHub Pages base path)
├── INBOUND OPEN.five9ivr   # Sample IVR script (auto-loaded)
├── src/
│   ├── main.js             # App entry point, file handling, UI wiring
│   ├── styles/
│   │   └── main.css        # Full design system (dark theme, animations, tooltip)
│   ├── parser/
│   │   ├── five9Parser.js  # Five9 XML → module graph
│   │   └── ttsDecoder.js   # TTS prompt text decoder
│   ├── data/
│   │   └── csvParser.js    # Call log CSV → heat map data
│   ├── scene/
│   │   ├── SceneManager.js    # Three.js orchestrator (scene, lights, camera, interactions)
│   │   ├── ModuleFactory.js   # 3D module geometry builder (10+ unique shapes)
│   │   ├── CableRenderer.js   # Orthogonal cable routing + flow particles + pulse waves
│   │   ├── AvatarController.js # 3rd-person character + smooth camera follow
│   │   └── ParticleSystem.js  # Dual-layer particle atmosphere (dust + fireflies)
│   └── ui/
│       ├── InspectorPanel.js  # Module detail sidebar
│       └── MiniMap.js         # 2D top-down overview minimap
```

## Deployment

### GitHub Pages
```bash
npm run build           # Build to dist/
npx gh-pages -d dist    # Deploy to gh-pages branch
```

### Manual Deploy
```bash
npm run build
# Upload contents of dist/ to any static host
```

## Contributing

Contributions are welcome! This is an open-source project — feel free to open issues, submit PRs, or fork and customize for your own IVR platform.

## License

MIT

---

<div align="center">
  <sub>Built with Three.js • Designed for Five9 IVR diagnostics • Open Source</sub>
</div>
