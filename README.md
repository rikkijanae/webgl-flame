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

- one **upward‑scrolling flow field** (built with iterative domain warping) feeds
  BOTH the flame shape and its colour, so when a flame pulls up its gradient pulls
  up with it — a single motion, not two. The colours curl and fold over one
  another in 3‑D, smooth everywhere, never striped,
- the **shape** is a flame‑density field carved from that flow into swoopy,
  never‑straight tongues, kept in the **bottom quarter** of the page,
- the **edge** is soft and slightly **blurred** into the page (not a hard clip),
- **rising ember specks** float up out of the fire and fade away, and a subtle
  **film grain** sits over the whole thing for texture and dimension,
- the **colour** runs a continuous blue → pink → red → orange → yellow → white
  palette with cool valleys, warm ridges, sheens and a brighter edge rim,
- the cursor locally lifts the fire, pulling flames and colour up together.

The cursor position is smoothed in JS and passed to the shader as a uniform. Touch
is supported too.
