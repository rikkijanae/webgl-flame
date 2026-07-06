# Flame

An interactive WebGL flame that burns on a pure‑white background — no black, anywhere.

The fire flickers and licks upward on its own, and leans toward your cursor as you
move the mouse near it. Colours are pulled directly from the source palette, ramped
by heat from the cooler outer wisps to the hottest core:

| Heat | Colour | Hex |
|------|--------|-----|
| coolest | amber | `#FFB724` |
| | orange | `#FF5A18` |
| | pink | `#F81A7D` |
| | red | `#F10B0A` |
| **hottest** | **blue** | `#37C2EC` |

Blue sits at the white‑hot core, exactly where a real flame is at its hottest.

## Run it

It's a single self‑contained file. Open `index.html` in any WebGL‑capable browser,
or serve it locally:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

## How it works

A full‑screen fragment shader builds the flame from layered value‑noise (fbm):

- a rising **domain warp** gives the curling, licking motion,
- a teardrop **body** narrows as it climbs,
- **turbulence** and a global flicker term animate the edges,
- a central **hot core** term drives the very centre up into blue,
- the heat value is mapped through a colour ramp and composited over white.

The cursor position is smoothed in JS and passed to the shader as a uniform, bending
the plume toward the mouse. Touch is supported too.
