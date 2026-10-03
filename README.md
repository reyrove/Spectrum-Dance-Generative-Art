# Spectrum Dance — Generative Art

> A seed-based generative system for dynamic curve compositions.  
> A reproducible catalogue of computational curve studies.

---

## What is this?

**Spectrum Dance** is a generative design system built on a chain of oscillating links. Each link is a control point that moves along its own sine wave — its own speed, its own amplitude, its own phase. The chain traces a single smooth curve, and the curve's colour drifts through the spectrum as the frame advances.

Every artwork in this catalogue is defined by a single numeric seed. The same seed always produces the identical composition — making each piece **traceable, reproducible, and licensable** across textile, print, and apparel applications.

Named for the continuous drift of colour and motion that characterises each composition, **Spectrum Dance** reframes animated curve generation as a textile.

---

## Live

🌐 **[View the catalogue →](https://reyrove.github.io/Spectrum-Dance/)**

---

## The System

The generator combines two layers:

| Layer | Description |
|-------|-------------|
| **Link chain** | 2 to 8 control points, each oscillating on its own sine wave. |
| **Colour drift** | The stroke colour drifts through the RGB spectrum on every frame, bounded by a seeded range. |

Both layers are driven by the same seed, ensuring deterministic output. The rendering is **live** — the cover, plate, and framed print all run continuous animation loops.

### Parameters

- **Control points** — 2 to 8
- **Link length** — `canvas size / (NumberOflinks × 2)`
- **Speed coefficients** — 10 to 50 (per link, per axis), signed at random
- **Initial phase** — 0 to 2π (per link), seeded
- **Angle velocity** — 1 / 20000 per frame
- **RGB range** — 1 to 10 per frame
- **Background gradient** — one of 180 curated tones on each end, drawn diagonally

---

## Structure

```
Spectrum-Dance/
├── index.html              ← Full catalogue (single-file)
├── images/
│   ├── fav.svg
│   ├── spectrum-tote.png
│   ├── spectrum-cushion.png
│   └── ...
├── Spectrum-Dance.jpg      ← Apparel mockup
└── README.md
```

The entire project is contained in a single `index.html` — no build step, no framework. The only external dependency is **p5.js** (loaded from CDN), which drives the exact curve-rendering pipeline.

---

## Features

- **Seed-based generation** — every composition is deterministic and reproducible
- **Live animation** — cover, plate, and framed print drift continuously
- **Live catalogue** — cover, statement, plate, surfaces, process, archive, commission sections
- **Multiple surfaces** — print, scarf, textile, wallpaper — all rendered from the same seed
- **Archive of 8 seeds** — click any plate to load it into the main view
- **PNG export** — download the current frame of the plate directly from the browser
- **Keyboard shortcuts** — `R` for new seed, `S` to save
- **Legal modal** — licensing, terms, and credits built in
- **Responsive** — works on desktop, tablet, and mobile
- **Mobile-first navbar** — horizontally scrollable with fade hint

---

## Usage

### Generate a new composition

Click **New Seed** or press `R`.

### Download the current frame

Click **Download** or press `S`.

### Load a seed from the archive

Click any plate in the **Archive** section.

---

## Color System

Every composition is seeded with two values:

- **Background gradient** — a two-tone diagonal gradient drawn from the same palette of 180 curated colours that the Arachne catalogue uses. Each seed picks two of them, one for the top-left, one for the bottom-right.
- **Stroke colour** — a seed initialises the starting RGB triplet. On every frame, each channel drifts by a random amount within `[-rgbRange, +rgbRange]`, then is clamped to `[0, 255]`. That gives the curve its "spectrum drift" — the colour continuously walks the RGB cube within a bounded neighbourhood.

Because the seed picks both the palette and the drift, no two seeds produce the same rhythm of colour.

---

## Technical Notes

- **p5.js** drives the curve rendering. The `beginShape()` / `curveVertex()` / `endShape()` pipeline is preserved exactly from the original design — the same Catmull-Rom spline, drawn with the exact same tangent math.
- **Seeded randomness** for structural parameters (link count, speeds, phases, initial colour) uses a Lehmer LCG. **Per-frame colour drift** uses `Math.random()`, matching the original file — because the drift is a live animation, not a seeded still.
- **Three independent p5 instances** run the cover, plate, and framed print. Each has its own canvas, its own seed, and its own animation loop.
- **Static stills for surfaces and archive.** Each of the four surfaces and eight archive thumbnails instantiates its own p5 sketch, runs it for a fixed number of frames (7000 for surfaces, 4000–12000 for archive), then calls `p.noLoop()` to freeze the composition.
- **No approximations.** Every canvas — live or frozen — uses the same p5 sketch factory. Nothing on the page renders a hand-rolled curve; every line you see comes from p5's `curveVertex`.
- **RAF pausing** — `visibilitychange` pauses all live p5 instances when the tab is hidden. Surfaces and archive are frozen already and don't need pausing.
- **Resize handling** debounces and fully rebuilds all p5 instances, so the composition always sizes correctly.
- `prefers-reduced-motion` respected.

---

## About

**Spectrum Dance** is a project by [Reyhaneh Daneshdoost](https://reyrove.github.io/) — an Iranian-born artist working at the intersection of classical textile logic and generative systems.

The work begins with a simple observation: the woven surface — repetitive, mathematically structured, infinitely variable — has always been a form of computation, long before computers.

**Spectrum Dance** is an attempt to render that logic visible.

> *A line that never stops moving cannot repeat — it can only return, shifted.*

---

## Licensing

All compositions are seed-documented and available for licensing across textile, surface, and apparel applications.

For commercial use, custom editions, or exclusive rights:

📧 **reyhanehdaneshdoost@gmail.com**

See the **Licensing** section in the live catalogue for details.

---

## Links

- 🌐 [Website](https://reyrove.github.io/)
- 📷 [Instagram](https://www.instagram.com/rey._.rove/)
- 💼 [LinkedIn](https://www.linkedin.com/in/reyhaneh-daneshdoost-730481160/)
- 🐦 [X](https://x.com/reyrove)

---

## Credits

**Design & Generative System**  
Reyhaneh Daneshdoost

**Typefaces**  
Cormorant Garamond · DM Mono

**Edition**  
Spectrum Dance — Autumn 2026

---

<p align="center">
  <em>Generative Dynamic Curve</em><br />
  <sub>© Reyrove Studio · All compositions reproducible by seed</sub>
</p>