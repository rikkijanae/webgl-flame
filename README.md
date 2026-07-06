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

A full‑screen fragment shader drives the flame from a single **twisting flow
field** — the same field shapes the silhouette *and* colours it, so the shape
swoops exactly with the gradient. Everything moves slowly for a silky slow‑fire
feel:

- the flow is built with **iterative domain warping** (the coordinate is folded
  through low‑octave noise several times), so colours curl and turn over one
  another in 3‑D like real flame — smooth everywhere, never striped or banded,
- the **shape** is a swoopy, never‑straight flame front driven by that same flow,
  confined to the **bottom quarter** of the page,
- the **colour** runs a continuous blue → pink → red → orange → yellow → white
  palette with cool blue valleys, warm ridges, white ridge sheens, and a brighter
  **rim gradient** right at the flame edge — giving it dimension,
- the **edge dissolves into the page** with a soft rim plus **tiny animated grain**
  that breaks it into embers, like real fire fading into the air,
- the cursor draws the flames upward toward it,
- a touch of dither removes any residual 8‑bit banding.

The cursor position is smoothed in JS and passed to the shader as a uniform. Touch
is supported too.
