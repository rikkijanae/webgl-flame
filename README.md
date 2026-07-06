# Flame

An interactive WebGL flame ribbon that burns across the bottom of a pure‑white
page — no black, anywhere. It flows silky‑smooth (think Stripe's gradient), fills
the bottom quarter of the viewport full‑width, and blends seamlessly with no
visible colour bands.

The fire drifts and breathes on its own, and the flames lean and rise toward your
cursor as you move near them. Colours come straight from the source palette,
ramped continuously by heat from the cool top edge down to the hottest base:

| Heat | Colour | Hex |
|------|--------|-----|
| coolest (top) | white | — |
| | amber | `#FFB724` |
| | orange | `#FF5A18` |
| | pink | `#F81A7D` |
| | red | `#F10B0A` |
| **hottest (base)** | **blue** | `#37C2EC` |

Blue sits at the white‑hot base, exactly where a real flame is at its hottest.

## Run it

It's a single self‑contained file. Open `index.html` in any WebGL‑capable browser,
or serve it locally:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

## How it works

A full‑screen fragment shader builds a **flame density field** and colours it:

- vertically‑stretched **value‑noise** (quintic‑smoothed fbm) scrolls upward and
  is pushed through a curling **domain‑warp**, giving tall, licking, swirling
  flame tongues that rise,
- a soft vertical envelope keeps the fire strong at the base and tapering as it
  climbs; a `smoothstep` on the density turns it into **solid flame bodies with
  soft edges that dissolve into white**,
- crucially, colour is driven by the **density (a 2‑D shape), not by height** — so
  hot and cool interleave along each flame like a real fire, instead of forming
  horizontal stripes,
- the densest cores near the base are the hottest and glow **blue**; edges cool
  through red → pink → orange → amber and fade out,
- the cursor bends the tongues toward it and feeds them extra height,
- a touch of dither removes any residual 8‑bit banding.

The cursor position is smoothed in JS and passed to the shader as a uniform. Touch
is supported too.
