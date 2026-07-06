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
with a **flowing striped gradient mesh**. Everything moves slowly for a silky,
slow‑fire feel:

- the shape comes from **smooth low‑octave value‑noise** (few octaves, quintic‑
  smoothed) stretched vertically and gently domain‑warped — clean curves, no
  high‑frequency fuzz; a full‑width solid base keeps the tongues one connected
  form,
- the edge is **hard‑clipped**: the density field is thresholded with a
  derivative‑based (`fwidth`) ~1‑pixel anti‑alias, so the silhouette is sharply
  defined — clipped, not a soft dissolve,
- the fill is a separate **stripe mesh**: two sets of clean colour bands running a
  cyclic palette blue → pink → red → orange → yellow → white, slowly waving and
  swinging their direction over time so the stripes travel in different directions
  while never breaking into random patches,
- the cursor bends the tongues toward it and feeds them extra height,
- a touch of dither removes any residual 8‑bit banding.

Requires the `OES_standard_derivatives` WebGL extension (universal on modern
browsers) for the hard edge.

The cursor position is smoothed in JS and passed to the shader as a uniform. Touch
is supported too.
