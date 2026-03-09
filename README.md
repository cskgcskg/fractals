# Fractal Explorer

A real-time, GPU-accelerated fractal explorer built as a single self-contained HTML file. Features 2D and 3D fractals, geometric patterns, interactive equation playground, and an educational mode exploring fractals in nature — all rendered via WebGL shaders with full zoom and navigation.

**[Launch the Explorer →](index.html)**

---

## Features

### 2D Fractals
Explore the classic complex-plane fractals with smooth iteration coloring and ultra-deep zoom (up to trillions of x magnification). Zoom targets cursor position for precise navigation into interesting regions.

- **Mandelbrot Set** — the iconic fractal with infinitely complex boundary
- **Julia Sets** — companion fractals with fixed c parameter
- **Burning Ship** — variant using absolute values, producing the distinctive "ship" shape
- **Tricorn** — conjugate variant with three-fold symmetry

Controls: iteration count (up to 2000), power (2–8), four color palettes.

### 3D Fractals
Raymarched 3D fractals with full orbit camera (drag to orbit, shift+drag to pan, scroll to zoom). Includes soft shadows, ambient occlusion, specular highlights, and orbit-trap coloring. Adaptive precision allows deep zoom up to 70,000x.

- **Mandelbulb** — the 3D analogue of the Mandelbrot set
- **3D Julia Set** — quaternion Julia fractal
- **Menger Sponge** — recursive cube subtraction
- **Sierpinski Tetrahedron** — recursive tetrahedral subdivision

Controls: power, iterations, detail level, four color palettes.

### Geometry
Interactive geometric patterns rendered as distance fields with configurable symmetry and complexity, all fully zoomable.

- **Kaleidoscope** — recursive symmetry folds with concentric detail
- **Spirograph** — hypotrochoid curves with nested inner patterns
- **Penrose** — five-fold quasi-crystalline tiling with golden ratio scaling
- **Apollonian Gasket** — recursive circle inversions producing fractal nesting

### Equations
An interactive Mandelbrot equation playground for learning how parameters shape fractals. A live equation display updates in real-time as you adjust sliders, showing the full mathematical breakdown.

- Toggle between **Mandelbrot** and **Julia** mode
- **Fractional power** (1.0–8.0 with 0.1 steps)
- **Complex c parameter** (real and imaginary sliders)
- **Escape radius** (2–50)
- **Iteration count** (32–1000)

The equation display shows `z_{n+1} = z_n^n + c` with live parameter values, initial conditions, and escape criteria — making visible how each slider changes the underlying mathematics.

### Learn
Seven nature-inspired fractal visualizations paired with rich educational content explaining the mathematics, real-world analogies, and where these patterns appear in the natural world.

| Topic | Visualization | Key Concept |
|-------|--------------|-------------|
| **Mountains** | FBM terrain with shadow mapping | Statistical self-similarity, fractal dimension, Mandelbrot's coastline paradox |
| **Ferns** | Recursive mirroring IFS | Barnsley's Fern, iterated function systems, exact self-similarity |
| **Lightning** | Ridged fractal noise | Diffusion-limited aggregation, Lichtenberg figures |
| **Cells** | Nested Voronoi diagrams | Voronoi tessellation, competitive growth, space-filling |
| **Forest** | Fractal tree branching with fBm canopy | Canopy fractal dimension, light harvesting optimization |
| **Lungs** | Bronchial tree with alveolar Voronoi | Murray's Law, 70 m² surface area, 23 generations of branching |
| **Activated Carbon** | Multi-scale nested pore structure | 3,000 m²/g surface area, macro/meso/micro/ultra pore hierarchy |

Each topic includes fact boxes, nature analogies with examples, "Try it" zoom prompts, and tags listing real-world occurrences.

---

## Technical Details

### Architecture
The entire application is a single `index.html` file with no external dependencies (except Google Fonts). All rendering is done via WebGL fragment shaders — one shader program per mode (2D, 3D, Geometry, Learn, Equations), compiled and linked at startup.

### Rendering Approach

- **2D modes** use complex-plane iteration rendered per-pixel in fragment shaders. The smooth iteration count algorithm provides continuous coloring without banding.
- **3D mode** uses **sphere-tracing (raymarching)** with signed distance functions. Each fractal type has a custom distance estimator. Lighting includes two-point diffuse, specular, soft shadows (48-step), ambient occlusion (5-tap), and rim lighting.
- **Geometry mode** renders distance fields of geometric constructions — kaleidoscopic folds, parametric curves, circle inversions.
- **Learn mode** combines multiple noise functions (fBm, ridged noise), Voronoi diagrams, and recursive distance fields to approximate natural phenomena.

### Adaptive Precision
All precision-dependent parameters (surface threshold, normal epsilon, shadow step size, AO scale) scale proportionally with camera distance, enabling deep zoom without artifacts. The 3D mode supports zoom down to `camDist = 0.00005` (70,000x), and 2D modes support zoom down to `10^-15` units per pixel.

### Performance
- Static 2D modes only redraw on parameter change (efficient)
- 3D mode renders continuously at full framerate
- DPR capped at 1.5 to maintain performance on high-DPI displays
- 200 raymarch steps, 48 shadow steps, 24 fractal iterations (configurable)

---

## Usage

Open `index.html` in any modern browser with WebGL support. No build step, server, or dependencies required.

### Controls

| Action | 2D / Geometry / Learn / Equations | 3D |
|--------|----------------------------------|-----|
| Navigate | Drag to pan | Drag to orbit |
| Zoom | Scroll (targets cursor) | Scroll |
| Pan | — | Shift + Drag |
| Reset | Reset View button | Switch fractal type |

Touch-screen support: single-finger drag to navigate, two-finger pinch to zoom.

---

## Color Palettes

Four color palettes shared across all modes, each built from hand-crafted gradient ramps:

- **Inferno** — deep black → crimson → orange → yellow → white-hot
- **Electric** — midnight → royal blue → cyan → white sparks  
- **Acid** — deep purple → magenta → toxic green → yellow
- **Frost** — deep navy → steel blue → ice → white → lavender

The Learn mode adds context-appropriate natural palettes (earth tones, greens, electric blues, warm organics, carbon grays) plus an X-Ray monochrome mode.

---

## Browser Support

Requires WebGL 1.0. Tested in Chrome, Firefox, Safari, and Edge. Mobile browsers are supported with touch controls.

---

## Credits

Built with [Claude](https://claude.ai) (Anthropic) — AI-assisted development of all WebGL shaders, fractal mathematics, UI design, and educational content.

## License

MIT License — free to use, modify, and distribute.
