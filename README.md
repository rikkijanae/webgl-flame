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

A full‑screen fragment shader builds a **solid flame silhouette** and fills it
with a **flowing gradient mesh**:

- vertically‑stretched **value‑noise** (quintic‑smoothed fbm) scrolls upward and
  is pushed through a curling **domain‑warp**, giving tall, licking flame tongues;
  a full‑width solid base keeps them a single connected form,
- a tight `smoothstep` on the density gives a **defined edge** — a solid shape
  sitting on the page, not a soft dissolve,
- the fill is a separate **gradient mesh**: soft wavy colour bands, warped and
  drifting upward, running a cyclic palette blue → pink → red → orange → yellow →
  white with extra white hotspots — a silky chromatic light‑leak,
- the cursor bends the tongues toward it and feeds them extra height,
- a touch of dither removes any residual 8‑bit banding.

The cursor position is smoothed in JS and passed to the shader as a uniform. Touch
is supported too.
