# OPNsense Multiverse — theme concept

A visual concept for an OPNsense theme with five palettes. This is a **mockup**,
not a finished theme and not an installable package. It exists to show what an
OPNsense theme *could* look like, and to invite discussion.

## What this is

A single self-contained HTML file that renders a fake OPNsense dashboard with
five switchable palettes:

- **Glass Dark** — dark, cyan accent, soft shadows (default)
- **Clean Light** — light, blue accent, flat
- **Neon Terminal** — near-black, green neon, monospace, square corners
- **Warm Slate** — warm dark grey, orange accent, larger radius
- **High Contrast** — black and white, yellow accent, thick borders

A dropdown in the top-right corner switches palettes live, without a reload.
The choice is remembered in `localStorage`.

## What this is not

- **Not a working OPNsense theme.** No `.pkg`, nothing to install.
- **Not 1:1 with the real OPNsense UI.** The mockup is plain HTML with its own
  classes. OPNsense runs Bootstrap 3 + AdminLTE with its own DOM, its own
  spacing and its own component set.

## Why it looks different from the real thing

OPNsense themes do not replace the stylesheet. A theme's `main.css` *is* the
whole stylesheet — Bootstrap included, 159 KB in 26.7 — and a custom theme
overrides it. That means:

- Colours, radii, shadows and fonts can be overridden almost completely.
- DOM structure, Bootstrap's grid, and dynamically generated widgets
  (DataTables, Select2, modals) cannot be replaced, only restyled.
- A 1:1 match with this mockup is not achievable through theming alone.
  Roughly 90% of the visual impression is, with a few dozen override rules.

## Trying it

Open `mockup.html` in any browser. Click the dropdown in the top-right corner.
Nothing is installed, nothing is sent anywhere.

## If someone wants to build this as a real theme

The pieces that matter:

- Palettes as CSS custom properties on `body`, with a `data-theme` override per
  palette. A default palette on `body` itself means the theme works with zero
  JavaScript, and `prefers-color-scheme` can pick the light palette
  automatically.
- `main.css` = base theme `main.css` + an override layer, not a replacement.
  The base's `build/` directory must be inherited whole, because `main.css`
  references `../fonts/` and `../images/` relatively.
- Bootstrap 3 selectors (`.content-box`, `.panel`, `.table`, `.btn-default`,
  `.label-*`) rather than Bootstrap 4 ones (`.badge-*`).
- The live switcher cannot ship inside the theme: OPNsense loads only CSS from
  a theme. A userscript, a browser extension, or separate per-palette packages
  are the options.

## Files
