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

A full‑screen fragment shader paints the ribbon:

- three layered, slow, low‑frequency **value‑noise** fields (quintic‑smoothed fbm)
  drift in different directions to give a silky, flowing motion,
- **heat** falls off up the bottom quarter of the screen, so every colour gets a
  generous slice of height,
- a gentle wavy **drift** makes the flame front breathe — faded out at the base so
  the blue foundation stays solid,
- the cursor adds a soft Gaussian **bump** to the heat, drawing the flames upward
  toward it,
- heat is mapped through a **wide, overlapping colour ramp** and a touch of dither
  is added to eliminate 8‑bit banding — so the whole thing reads as one seamless
  gradient instead of contour lines.

The cursor position is smoothed in JS and passed to the shader as a uniform. Touch
is supported too.
