# The Collatz Conjecture — an interactive visual essay

Take any whole number. Halve it if it is even; triple it and add one if it is odd.
Repeat. Every number ever tried has fallen to 1 — and after nearly a century, no
one can prove they all must.

This is a single-file, zero-dependency web page that makes that mystery visible.
Everything on the page is computed live in your browser.

## What's inside

- **The Collatz coral** — 1,300 complete orbits drawn in reverse from the root
  outward. At each step the line bends one way for an even number and the other
  way for an odd one (an idea from mathematician Edmund Harriss). Superimposed
  with additive glow on `<canvas>`, the orbits grow into an organic coral-like
  form on page load. A *bend* slider and *Regrow* button reshape it.
- **Hailstone trajectory explorer** — type any starting number and watch its
  orbit on a log-scale chart, with the peak marked, a crosshair tooltip, stat
  tiles (steps, highest point, odd "climb" steps), and the full sequence
  readout. Computation uses `BigInt`, so the preset `989345275647` — 1,348
  steps, peaking at 1,219,624,271,099,764 — is exact.
- **Stopping-time scatter** — total stopping time for every `n` from 1 to
  10,000. The drifting bands emerge on their own; record holders (27, 703,
  6171, …) are found at runtime, marked in rose, and listed in a table.
- **The story** — the rule, the hailstone name, the 2⁷¹ verification bound,
  Terence Tao's 2019 "almost all" result, and Erdős's verdict.

## Run it

No build step, no dependencies. Either open `index.html` directly, or serve it:

```sh
python3 -m http.server 8000
# then open http://localhost:8000
```

## Publish with GitHub Pages

1. Push this repository to GitHub.
2. In the repo: **Settings → Pages → Source**, choose **Deploy from a branch**,
   select `main` and `/ (root)`, and save.
3. The page appears at `https://<username>.github.io/<repo>/`.

## Implementation notes

- One HTML file: all CSS and JavaScript inline, no external requests of any kind.
- The coral precomputes every orbit's polyline, fits the bounding box to the
  viewport, then animates growth frame-by-frame into an offscreen canvas; a
  quarter-resolution upscale pass provides cheap bloom.
- Charts are hand-built SVG (trajectory) and canvas (scatter) with hover
  tooltips; no charting library.
- Honors `prefers-reduced-motion` (renders the finished coral instantly) and
  keeps keyboard focus visible on all controls.
- Chart colors were validated for color-vision-deficiency separation and WCAG
  contrast against the panel surface.

## Credits

- Coral rendering idea after Edmund Harriss's Collatz visualisations.
- Verification bound from David Barína's 2⁷¹ computational project.
