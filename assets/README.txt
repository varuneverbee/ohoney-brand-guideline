Ohoney logo assets — approved set
=================================

14 files, extracted from the Ohoney Brand Guide. Every file is byte-identical to
the source in the Ohoney repository (verified by SHA-256). No retired or
incorrect asset is included.

logo/     The full lockup — mark + "Ohoney" wordmark.
  ohoney-logo-light.svg   Light backgrounds. The "O" is warm brown #20170d.
  ohoney-logo-dark.svg    Dark backgrounds. The "O" is warm cream #fdfaf3.
  ohoney-logo-mono.svg    Single colour; inherits currentColor. For engraving,
                          embossing, one-colour print, watermarks, and for
                          placing on brand orange or the brand gradient.

icon/     The honey dipper mark alone. Use below 64px wide, where the wordmark
          falls under its minimum size.
  ohoney-icon.svg         Brand orange. Works on both light and dark grounds.
  ohoney-icon-mono.svg    Single colour; inherits currentColor.

favicon/  Browser tab. Transparent — no tile, so the mark sits on the browser's
          own chrome.
  favicon.svg             Primary. Crisp at any DPI.
  favicon.ico             Fallback (16/32/48) for browsers that won't take SVG.
  favicon-16x16.png       Raster fallback.
  favicon-32x32.png       Raster fallback, retina.

app-icon/ Installed apps. These keep an opaque #20170d tile on purpose: a
          transparent PNG is composited unpredictably by iOS and is invalid as
          an Android maskable icon.
  apple-touch-icon.png       180px, iOS home screen.
  icon-192x192.png           Web app manifest.
  icon-512x512.png           Web app manifest, splash screens.
  icon-maskable-512x512.png  Android maskable; full-bleed square, the platform
                             applies its own mask.

social/
  social-preview.png      1200x630 Open Graph / Twitter card image.

The three rules that matter most
--------------------------------
1. Match the variant to the background. The light lockup on a dark ground
   leaves the "O" at 1:1 contrast — effectively invisible.
2. Below 64px wide, drop the wordmark and use the icon.
3. Keep clear space of 1x (preferred) or 0.5x (minimum) the height of the "O"
   on all sides — the "O" is 60.6% of the lockup's full height.

Do not stretch, rotate, crop, recolour, or add shadow/glow to these files, and
do not typeset "Ohoney" in another face to stand in for the wordmark.

Full guide, including correct/incorrect examples:
https://github.com/varuneverbee/ohoney-brand-guideline
