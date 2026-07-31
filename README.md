# CADHAUS

> **View, edit, and export CAD files right in your browser — nothing to install.**

CADHAUS is a single self-contained HTML file that turns any modern browser into a lightweight CAD workstation. Drop in a 2D drawing or a 3D model, look it over, make quick edits, and export the result — all offline for common formats, with no accounts, no uploads to a server, and no build step.

It's built for the moment you're handed a `.dxf`, `.stl`, `.obj`, or `.step` file and just need to *see it, tweak it, and get a PDF out* — without opening heavyweight desktop CAD software. The interface is English-first with a one-tap Korean toggle (**EN · KO**), and the whole app runs happily on free static hosting like GitHub Pages.

**Live demo:** enable GitHub Pages on this repo (see below) and it runs at `https://<your-username>.github.io/CADHAUS/`.

---

## Features

**2D — DXF**
- Open DXF drawings: lines, circles, arcs, polylines, and text
- Pan, zoom, grid snap
- Select and drag to move, delete, undo (Ctrl+Z)
- Draw lines, rectangles, circles, and text
- Two-point dimension measurement
- Edit radius and text content numerically in the side panel

**3D — STL · OBJ · STEP**
- STL (ASCII & binary) and OBJ load instantly, offline
- STEP (`.stp` / `.step`) via the OpenCascade WASM engine (loaded on demand)
- Orbit, zoom, pan
- Change color, toggle wireframe, rotate X/Y/Z 90°, scale

**Export**
- DXF (2D) and STL (3D) with edits applied
- PNG snapshot
- PDF — 2D renders as a clean black-on-white print sheet with filename and date

**Bilingual** — English by default, Korean via the EN · KO button. All labels, tooltips, and status messages switch live.

---

## Format support & limits

| Format | Read | Notes |
|---|---|---|
| DXF | ✅ | Blocks/INSERT, hatch, and splines not yet supported |
| STL | ✅ | ASCII and binary |
| OBJ | ✅ | Triangulated on load |
| STEP / STP | ✅ | Requires internet on first use (downloads a ~10 MB WASM engine) |
| DWG | ❌ | Proprietary binary — convert to DXF first (AutoCAD, or free ODA File Converter) |

STEP is imported as a mesh for viewing and format conversion — parametric/B-rep editing is out of scope.

---

## Run locally

Just open the file. Because STEP loads its engine over the network and browsers restrict `file://` requests, use a tiny local server for full functionality:

```bash
# Python 3
python3 -m http.server 8080
# then open http://localhost:8080

# or Node
npx serve
```

DXF, STL, and OBJ work fine even from a plain `file://` open.

---

## Deploy to GitHub Pages

1. Push this repository to GitHub.
2. **Settings → Pages → Build and deployment → Source: Deploy from a branch.**
3. Branch: `main`, folder: `/ (root)`. Save.
4. Wait ~1 minute, then visit `https://<your-username>.github.io/CADHAUS/`.

The app is the root `index.html`, so no configuration is needed.

---

## Tech

- [three.js](https://threejs.org/) r128 — 3D rendering
- [occt-import-js](https://github.com/kovacsv/occt-import-js) — STEP import (OpenCascade WASM)
- [jsPDF](https://github.com/parallax/jsPDF) — PDF export
- Plain HTML/CSS/JS — no framework, no build

All third-party libraries load from CDN; the app itself is one self-contained HTML file.

---

## License

MIT — see [LICENSE](LICENSE).
