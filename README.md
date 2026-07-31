# Ohoney Brand Guideline

The approved Ohoney logo system: usage rules, light/dark/mono variants, clear
space, minimum size, colors, and the complete favicon / app-icon set.

## Contents

| Path | What it is |
|---|---|
| [`brand-guide.html`](brand-guide.html) | The interactive guide. Open it directly in any browser — no server, no install, no network access needed. Every asset and download is embedded in the file. |
| [`BRAND.md`](BRAND.md) | The full written brand system: voice, visual rules, components, motion. |
| [`assets/`](assets) | The 14 approved logo, icon, and favicon files, also downloadable from inside the guide. |

## Quick rules

- **Variant matches the ground.** `ohoney-logo-light.svg` on light backgrounds,
  `ohoney-logo-dark.svg` on dark. The upright "O" is warm brown on light and warm
  cream on dark — never neutral black or white, and never the wrong pairing.
- **Below 64px wide, use the icon**, not the wordmark.
- **Clear space** is 1x (preferred) to 0.5x (minimum) of the "O"'s height, on all
  sides.
- **No PNG exports of the lockup.** It's SVG-only, deliberately — resolution
  independent, no font dependency.
- Full detail, including the "why" behind each rule, is in `brand-guide.html`.

## Source of truth

These files are exported from the Ohoney app's own design system
(`apps/web/src/shared/ui/logo-geometry.json` and
`apps/web/scripts/generate-brand-assets.mjs` in the main Ohoney repository).
This repo is the distribution copy for partners and external use — the
generator, not this repo, is where the mark itself is edited.
