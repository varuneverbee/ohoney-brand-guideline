# BRAND.md — Ohoney

**This is the single source of truth for Ohoney's brand and visual identity.**
Engineers and Claude Code MUST consult this file before any UI, copy, or asset
work. If something here conflicts with what you see in code, the conflict is
a bug — flag it.

Strategic context (positioning, full BrandScript, voice rationale, decision
log) lives in [brand-brief.md](brand-brief.md). This file is the
distilled, engineer-facing version: do this / don't do this.

> **Scope exception — the internal admin console.** The operator-only admin
> console in `apps/web` (`/admin` route tree: credits, pricing, plans, global
> settings) is **exempt from this file** (decided 2026-07-08). It is internal
> tooling, never seller-facing: no brand tokens, no wordmark, no voice rules,
> no mobile-first requirement. Its look-and-feel follows the admin-dashboard
> reference artifact (light theme), documented in the admin design spec under
> `docs/superpowers/specs/`. The `/admin` row in the surfaces tables below
> refers to the legacy prototype admin page, not this console.

**Live brand kit:** [`/brand`](public/brand/index.html) — at
`http://localhost:8000/brand`. Renders every component with production CSS.
Mission, ICP, voice, color, type, components, motion, partner logos — one
scrollable reference. The visual companion to this file.

---

## Before you commit any UI / copy change — 10-second checklist

1. **Wordmark.** Did you render the brand name as `O<i>honey</i>` (capital O upright, "honey" italic)? Never `OHoney`. Never `OHONEY`.
2. **Primary color.** Did you use `var(--brand)` (= `#ef7d2b`)? Not raw hex. Not the old indigo `#6366f1`.
3. **Voice.** Does your copy avoid the [banned words](#voice---banned-words) list — especially `ship`, named competitors, `leverage`, `empower`, `cutting-edge`, `seamless`?
4. **Sellers' vocabulary.** Are you saying `list / post / launch / drop / publish / generate` instead of `ship`?
5. **Surface.** If marketing page, did you put it on `body.landing-dark` with grain + mesh blobs? If in-app, did you stay on the light, flat workspace surface?
6. **Motion.** Does every animation honor `@media (prefers-reduced-motion: reduce)`?
7. **Imagery.** Are product previews composited onto warm-cream cards, not floating as raw transparent PNGs?
8. **Icons.** Stroked, 1.5–2.4 stroke-width, `currentColor`. Inline SVG, never an icon font.
9. **Heritage line.** When you mention provenance, say "Built by the EverBee team" — not "powered by," not "from the makers of."
10. **Conflict?** If the design feels like it wants to break a rule here, that's a brand decision — escalate (Cody), don't silently override.

---

## Wordmark + Logo

| Element | Rule |
|---|---|
| Spelling | `Ohoney` — capital O, lowercase honey. Never `OHoney`, never `Oh Honey`, never `OHONEY`. |
| Emphasis | `honey` is set apart from the upright `O`. In prose that is italics; in the logo the orange-to-pink gradient carries it and the letterforms stay upright. **Open question for Cody — see the note below this table.** |
| Rendering (app) | `<Logo />` from `apps/web/src/shared/ui/logo.tsx` — the only implementation. Mark *and* wordmark are one SVG; the wordmark is outlined Inter SemiBold, not live text. |
| The `O` | Warm brown `--color-ink` `#20170d` on light grounds, warm cream `--color-cream` `#fdfaf3` on dark. The pair stays in the brand's warm family rather than neutral black/white, and both clear 16.9:1. |
| The `honey` gradient | Always `--color-brand` `#ef7d2b` → pink, at 135°. Ends on `--color-pink-deep` `#db2777` on light grounds and `--color-pink` `#ec4899` on dark. |
| Logo mark | `<Logo type="icon" />`, or `/assets/brand/ohoney-icon.svg` where a URL is needed. Brand orange on every ground. |
| Standalone files | `/assets/brand/ohoney-logo-{light,dark,mono}.svg` and `ohoney-icon{,-mono}.svg`. Generated — run `pnpm --filter @ohoney/web brand:assets`, never hand-edit. |
| Favicon / browser tab | `/assets/brand/favicon.svg` + `favicon.ico` (16/32/48) + `favicon-{16,32}x{16,32}.png`. **Transparent — no tile**, brand mark cut at 92% of the canvas so it holds its own directly on the browser's chrome. |
| App icons | `apple-touch-icon.png`, `icon-{192,512}x{192,512}.png`, `icon-maskable-512x512.png`. These **keep an opaque `#20170d` tile** (6.4:1): a transparent PNG is composited unpredictably by iOS and is invalid as an Android maskable. |
| Mark alone | OK for favicon and app-icon contexts only. Marketing surfaces use wordmark + mark together. |
| Clear space | Min height for the logo lockup = 16px (`<Logo size="sm" />`). Nav renders 24px (`lg`). |
| Pronunciation in copy | "Oh, honey" — the affectionate aside, not an exclamation. Never write it that way; let the wordmark imply it. |

> **Open question (2026-07-29).** This file has always said "italic on `honey`", but no
> shipped lockup has ever rendered it that way — the old marketing CSS set
> `font-style: normal` on the `<i>`, and the sidebar used a plain `<span>`. The new
> `<Logo />` preserves that upright-plus-gradient treatment. Prose instances
> ("Welcome to O*honey*") do still italicise. Cody to confirm which is canonical for
> the logo; nothing was changed unilaterally.

---

## Color tokens — use the CSS variables, not raw hex

All color tokens live in `public/styles.css` under either the default `:root`
(light app surface) or the `body.landing-dark` block (dark marketing surface).
Never inline hex when a variable exists.

### Brand
| Token | Light | Dark |
|---|---|---|
| `--brand` | `#ef7d2b` | `#ef7d2b` |
| `--brand-soft` | `#fff4eb` | `rgba(239, 125, 43, 0.10)` |
| `--brand-border` | `#fcd9b6` | `rgba(239, 125, 43, 0.32)` |
| `--brand-deep` | `#9c4612` | `#f97316` |

`--warm*` is a legacy alias of `--brand*` — both resolve to the same values.
Prefer `--brand` in new code.

### Supporting brand
| Token | Hex | Use |
|---|---|---|
| `--pink` | `#ec4899` | Hero word gradient, mesh-blob-b, accent highlights |
| `--violet` | `#a855f7` | Hero word gradient, mesh-blob-c, EverBee tie-in |
| `--cyan` | `#22d3ee` | Dark-theme only. Mesh-blob-d, occasional spark accent. |

### Semantic
| Token | Light | Dark | Use |
|---|---|---|---|
| `--good` | `#10b981` | `#34d399` | Success states, "approved" badges |
| `--bad` | `#ef4444` | `#ef4444` | Error states, "broken / cost" callouts |

### Neutrals — light (default app surface)
| Token | Value |
|---|---|
| `--bg` | `#fafafa` |
| `--bg-card` | `#ffffff` |
| `--bg-soft` | `#f4f4f5` |
| `--text` | `#111` |
| `--text-soft` | `#666` |
| `--text-faint` | `#888` |
| `--border` | `#ececec` |
| `--border-strong` | `#e5e5e5` |
| `--line` | `rgba(0, 0, 0, 0.08)` |

### Neutrals — dark (`body.landing-dark`, marketing pages)
| Token | Value |
|---|---|
| `--bg` | `#0a0a0f` |
| `--bg-soft` | `#14141c` |
| `--bg-card` | `rgba(255, 255, 255, 0.03)` |
| `--bg-elevated` | `#1a1a24` |
| `--text` | `#f5f5f7` |
| `--text-soft` | `#a1a1aa` |
| `--text-faint` | `#71717a` |
| `--line` | `rgba(255, 255, 255, 0.08)` |

---

## Typography

```css
font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", system-ui, sans-serif;
/* Mono */
font-family: ui-monospace, "SF Mono", Menlo, monospace;
```

- **No webfont loads.** Bun-native, zero-dep velocity is load-bearing (see CLAUDE.md). Don't add Google Fonts without a real reason.
- **Italic on `honey`** inside the wordmark is the lone typographic flourish.
- **Body sizes:** 13–16px is the default workspace range. Hero headlines clamp(40px, 7vw, 80px).
- **Mono** is for code, hex values, IDs, prompt-editor textareas — never body copy.

---

## Radii + shape

| Use | Radius |
|---|---|
| Pills (status chips, CTAs that want to feel pressable, niche tags) | `999px` |
| Inputs (text, select) | `8px–10px` |
| Buttons | `10px` |
| Cards | `12px–16px` |
| Avatars | `50%` |

Soft but not toy-rounded. If a rectangle has corners < 8px, it's probably a
table cell or a divider — that's fine.

---

## Surfaces — which theme goes where

| Surface | Body class | Theme |
|---|---|---|
| Marketing (`/`, landing, pricing, about) | `body.landing-dark` | Dark + grain + 4 mesh blobs |
| In-app workspace (`/create`, `/admin`, `/templates`, `/discover`) | default `<body>` | Light, flat, no texture |
| Sub-product surfaces (ad-studio, edit) | default `<body>` | Light, flat |

**Don't mix.** Marketing texture inside the workspace makes the app feel slow and decorative. Workspace flatness on the marketing page makes the brand feel small.

---

## Voice — vocabulary

Full rationale in [brand-brief.md](brand-brief.md) under `voice:`. Quick rules:

### Use (seller-native action verbs)
`list · post · launch · drop · publish · generate · fix`

### Use (after-state words)
`polished · on-brand · consistent · in minutes`

### Use (empathy openers)
`we get it · we built this because · we've been there`

### Use (concrete numbers)
`30 seconds · 50 listings · 5 storefronts · 1M+ sellers`

### Voice — banned words
| Banned | Why | Replace with |
|---|---|---|
| `ship` | SaaS/dev jargon. Sellers don't say it. (Saved as durable feedback `feedback_seller_vocab_no_ship`.) | `list / post / launch / drop / publish` |
| Named competitors (`Canva`, `Placeit`, `Midjourney`, `Photoroom`, `Fiverr`) in marketing copy | Cody's rule: don't name people on the journey who haven't been told yet. (Saved as `feedback_no_competitor_naming`.) | Categories: "general-purpose design tools," "single-model AI generators," "freelance hires." |
| `leverage · empower · seamless · holistic · cutting-edge · innovative · solutions · transform · revolutionary · 10X · GTM · ship velocity` | Generic SaaS slop. Fails the swap test (any product could claim it). | Concrete numbers + concrete actions. |
| `darling · sweetie · babe · magical · supercharged · next-level · easy peasy · just sign up` | Patronizing, hype, or saccharine. Despite the brand name, we don't pile on warmth. | Warm but matter-of-fact tone. |
| `GenAI · LLM · diffusion model · prompt engineering` in seller-facing copy | Jargon sellers don't use. | "AI" or specific model names ("Veo 3 video," "Gemini 2.5") — sellers understand model names as branded features. |

### Voice — dimensions (NN/g)
- **Funny ↔ Serious:** −1 (slightly serious, never goofy)
- **Formal ↔ Casual:** −2 (clearly casual)
- **Respectful ↔ Irreverent:** −1 (slightly playful, never disrespectful)
- **Enthusiastic ↔ Matter-of-fact:** −1 (slightly matter-of-fact)

### Sounds like
- Mailchimp circa 2017
- A friend who runs her own Etsy shop and just figured out the design problem
- Someone who's done it 10,000 times explaining it to someone doing it for the first time

### Does NOT sound like
- Corporate AI press release ("breakthrough," "REVOLUTIONIZE")
- Bro-y SaaS pitch deck ("10X your workflow")
- Grandma's email forward (saccharine, ellipses)
- Photoshop's technical docs (intimidating, tech-first)

---

## Heritage line

When provenance is mentioned, use one of these. Don't improvise.

- "Built by the EverBee team."
- "Built by the EverBee team, where 1M+ Etsy sellers already start their day."
- "© Ohoney · A product by EverBee" (footer-style)

Avoid: "powered by EverBee," "from the makers of EverBee," "an EverBee product"
(too distant), "by Cody McGuffie" (too founder-as-hero).

---

## Imagery + motion

### Imagery rules
- **Product previews** = real photography composited onto warm-cream cards (`linear-gradient(155deg, #f7f3e9, #ece5d3)`). Never raw transparent PNGs on dark — they look broken (v6 decision log).
- **Hero scenes** = niche → keyword → live design generation, framed as workflow not gallery.
- **No lifestyle stock photography.** Ever. We sell to sellers, not aesthetes.
- **Mockups** = product on solid color, framed by the brand-card surface. The Recolor scene is the reference: t-shirts on swatches, color-fan-out.

### Motion rules
- Primary easing: `cubic-bezier(0.16, 1, 0.3, 1)` — gentle out-cubic
- Spring easing: `cubic-bezier(0.34, 1.56, 0.64, 1)` — for chips/badges popping in
- Staggered reveal-on-scroll is the dominant pattern (every section uses it)
- Mesh blobs drift; nothing strobes
- **EVERY animation must include `@media (prefers-reduced-motion: reduce) { animation: none; opacity: 1; }` fallback**
- **In-app interactive motion** (reactive cards, incubate/hatch, reveal-on-load) is its own shared system — see [§ Motion — the alive system](#motion--the-alive-system) below. Don't reinvent per-page; it's global via `side-nav.js`.

### Texture rules
- `.landing-grain` overlay on `body.landing-dark` only
- 4 mesh blobs (`.mesh-blob-a/b/c/d`) — honey, pink, violet, cyan, blurred
- In-app surfaces stay flat — no texture, no blobs

---

## Motion — the alive system

The in-app workspace uses a single shared motion layer so the product feels
like a living, breathing organism that works for the seller — not a static
form. It lives in **`public/motion.css`** + **`public/motion.js`** (served at
`/motion.css` + `/motion.js`) and is **injected on every in-app page by
`side-nav.js`** — any page that mounts the side-nav gets it automatically.
Don't add motion `<link>`/`<script>` tags per page; they're global.

**Governing principle: calm by default, alive on activity and intent.** The
app stays quiet until it's either working for you or being touched. "Alive"
must never tip into "busy."

### The four behaviors

| Behavior | What it does | Where |
|---|---|---|
| **Reactive hover** | Content cards lift, tilt ≤1.4° toward the cursor, and a honey glow tracks the pointer | Every browsable content card, app-wide |
| **Reveal on load** | Content cards rise in (fade + 10px), staggered, on first paint | Every in-app page, initial load only |
| **Incubate → hatch** | Generation skeletons gestate in honey; each finished design holds the shimmer until ITS image loads, then springs in + a honey ring bursts | Create generation grids (`.motion-reactive`) |
| **Magnetic** | Element leans toward the cursor when near | Opt-in: `[data-magnetic]` |

### What reacts and what stays calm

Reactive hover applies only to **browsable content cards**. The curated
selector set lives in `motion.js` (`CARDS`):
`.tile · .disc-card · .disc-insp-card · .conn-card · .conn-cat-tile ·
.conn-add-tile · .conn-modal-tile · .bk-store-card · .bk-workspace-card ·
.template-card · .dev-feature-card · .dev-quicklink · .pick`

**Deliberately NOT reactive** (they'd feel wrong tilting under the cursor):
data/KPI cards (`.admin-cogs-card`), form rows (`.keys-row`, `.ws-card`),
and the image-editor canvas. When you add a new browsable card type, add its
class to `CARDS` in `motion.js` — don't add tilt to data or form surfaces.

### Implementation rules

- **Transform/opacity only** — GPU-cheap. Never animate layout properties.
- **Glow is a conflict-free injected `.motion-glow` layer**, not `::after` —
  so it works on any card type without clobbering existing pseudo-elements.
- **Tilt is subtle (≤1.4°)** and auto-pauses when a menu inside the card is
  open, so dropdowns don't wobble.
- **Reveal is one-time** (initial-load window) and capped — it never
  re-animates on filter changes / pagination, and never janks a huge list.
- **Eases:** reactive/reveal use the primary out-cubic; hatch uses the spring
  (see Motion rules above).
- **`prefers-reduced-motion` is a hard off-switch** for the entire layer.

### Progress = honey, not green

In-flight/working state reads in **brand honey** (`--brand-soft` pill, `--brand`
dot), matching the incubate/hatch language — not green. Green (`--good`) is for
success/approved only, never "in progress." See `.progress` in `styles.css`.

### Proposed (parked): mouse-reactive aurora background

A living, cursor-following background for Ohoney's dramatic **dark** surfaces
(future marketing / landing / onboarding) — the honey light follows the mouse.
Derived from oposhop's `.page-wash` (drifting radial mesh + grain), rebuilt
**vanilla** (no Three.js) and recolored honey → amber → pink (never oposhop
purple). Approved as a direction, **not yet integrated.** Working demo:
[`/assets/motion/aurora.html`](public/assets/motion/aurora.html). Full pickup
notes in [BACKLOG.md](BACKLOG.md) § "Brand / motion". Rule of thumb if/when it
ships: full aurora on dark marketing only; in-app cream stays calm (a much
subtler variant at most).

---

## Iconography

- **Library:** Lucide-style stroked icons. Inline SVG, copied into HTML directly.
- **Stroke width:** 1.5–2.4 (most usage = 2)
- **Fill:** `none`
- **Stroke:** `currentColor` (inherits from text color)
- **Line caps/joins:** `round`
- **Sizes:** 14, 16, 20, 24 px. Standard nav icon = 16.
- **Never** use an icon font (FontAwesome, Material). Bun-native, zero-dep.

---

## Components — canonical patterns

These live in `public/styles.css` and `public/landing.html`. Reuse, don't reinvent.

| Pattern | Class / token | Where it lives |
|---|---|---|
| Hero gradient word | `.landing-h1` with reveal animations | landing.html ~line 60 |
| Pill chip (status, counter) | `.hero-pill`, `.hero-pill-dot`, `.hero-pill-counter` | styles.css `.hero-pill` |
| Primary CTA | `.landing-nav-cta` | landing.html nav |
| Card grid | `.builtfor-grid` + `.builtfor-card` | landing.html ~line 280 |
| Niche/keyword chip | `.builtfor-platforms` chip row | landing.html "Built for" section |
| Old/Ohoney compare | `.problem-compare` + `.problem-col` | landing.html ~line 160 |
| Tile (hero product grid) | `.hero-product-grid .hero-tile.state-done` | styles.css |
| Mesh blob | `.mesh-blob.mesh-blob-{a,b,c,d}` | styles.css, landing.html |
| Workspace card | `.bg-card` + `--border` + `--radius: 12px` (light theme) | styles.css `:root` |

Before adding a new component, grep `public/styles.css` for an existing
pattern that fits. If you genuinely need a new one, add it to this table
in the same PR.

---

## Provider / model names (when listed in marketing)

Marketing copy lists the 12-model lineup by **real model names**, not the
internal `Painter/Studio/Vector/Sharp/Sketch` code-names:

- **Image:** Gemini 2.5 Flash Image · Recraft v3 · Imagen 4 · Ideogram v3 · GPT Image 1 · Pollinations Flux
- **Video:** Runway Gen-3 Turbo · Seedance 2.0 · Veo 3 · WAN 2.5
- **Utility:** BiRefNet (background remove) · Real-ESRGAN (upscale)

Internal code may still use the code-names — they're a `src/prompts.ts` /
`gemini.ts` concern, not a marketing concern.

### AI model-provider logos (model picker)

The in-app model picker (`#model-peek`, rendered by `renderModelPeek()` in
`public/app.js`) shows each engine's **real provider logo** on a white tile
instead of the old `✦` sparkle. Assets live in
[`/public/assets/brand-logos/`](public/assets/brand-logos/); the
`MODEL_LOGOS` map in `app.js` keys them by provider `id` (see
`src/providers/registry.ts`). The virtual `default`/Auto router keeps the
sparkle (no provider).

| Provider id | Picker label | Logo file | Source |
|---|---|---|---|
| `gemini` | Gemini | `gemini.svg` | svgl (gradient star) |
| `openai` | OpenAI | `openai.svg` | svgl (blossom) |
| `recraft` | Recraft | `recraft.png` | recraft.ai favicon |
| `ideogram` | Ideogram | `ideogram.png` | ideogram.ai favicon |
| `pollinations` | Pollinations | `pollinations.png` | pollinations.ai apple-touch-icon |
| `fal-flux-pro` / `-schnell` / `-kontext` | FLUX | `flux.png` | Black Forest Labs (bfl.ai) favicon |
| `fal-imagen4` | Imagen 4 Ultra | `google.svg` | svgl (Google "G" — Imagen is a Google model) |
| `fal-clarity` | Clarity Upscaler | `clarity.svg` | custom glyph (no brand logo exists) |

To add a model logo: drop the asset in `brand-logos/`, add a `MODEL_LOGOS`
entry in `app.js`, done. Tile styling is `.model-peek-avatar.has-logo` in
`styles.css` (white tile, 6px inset, `object-fit: contain`). **No TikTok
asset exists** — if a video/TikTok engine ever needs a mark, source one first.

---

## Platform partners — colors for badges

When rendering platform chips (e.g. on "Built for" cards), use the platform's
own brand color:

| Platform | Color | Notes |
|---|---|---|
| Etsy | `#f1641e` | |
| TikTok Shop | `#161823` | (TikTok dark — could swap to brand-accurate pink/cyan if requested) |
| OpoShop | `#7c3aed` | EverBee purple |
| Shopify | `#95bf47` | |
| Printful | `#1f72b8` | |
| Printify | `#2eb872` | |

---

## Tagline + key copy

| Use | Copy |
|---|---|
| Primary tagline | **Design like your business depends on it.** |
| Trueline (sub-headline) | The only AI design tool where every model was picked because sellers need it — not to make the tool sound impressive. |
| Onliness statement | Ohoney is the only AI creative studio built for online sellers — with photo, vector, sharp-text, and Veo 3 video models in one workspace, wired into the listing research sellers already use. |
| Primary CTA | **Start designing free** |
| Secondary CTA | **See pricing** |
| Heritage tagline | Built by the EverBee team, where 1M+ Etsy sellers already start their day. |

Don't paraphrase these without checking the [decision log](brand-brief.md#decision-log) — most have been tested through multiple rounds of edits.

---

## In-app design system (editorial cream surface)

The in-app workspace pages (`/connections`, `/pipeline-app`, future `/discover`,
`/automations`) share an editorial visual language: cream surface, brand-honey
accents, system-serif heading stack with one italic word per heading. This is
distinct from the marketing landing-page treatment (which is dark + grain + mesh
blobs). Both are correct for their context — don't mix.

Live demo + canonical reference: [`/brand`](public/brand/index.html).
Pattern CSS: [`public/connections/connections-b2.css`](public/connections/connections-b2.css)
(named for its origin in F2 design-shotgun pick — extends to all in-app pages).

### Heading rhythm — one italic word

H1 / H2 always have exactly one word in italic + brand orange. That italic
accent is the visual signature. Don't italicize multiple words. Don't accent
non-italic.

```html
<h1>The connections that <i>power</i> your work.</h1>
<h2>Where your brand <i>lives</i>.</h2>
<h3>Live <i>product feed</i></h3>   <!-- H3 = whole heading italic, no orange -->
```

Font stack — system serif, no webfont load:

```css
--font-heading: 'Iowan Old Style', 'Charter', 'Georgia', serif;
```

### Component patterns

| Pattern | Class | Notes |
|---|---|---|
| Workspace card | `.conn-card` | Full template: header + KPIs + product feed + footer |
| Default-connection card | `.conn-card.is-default` | Always-on (EverBee Research, Brand Kit). No KPIs, italic blurb instead |
| Add-tile (more) | `.conn-add-tile` | Dashed border, brand-honey hover |
| Inline catalog tile | `.conn-cat-tile` | Used in empty state + modal |
| Modal tile | `.conn-modal-tile` | Picker tile inside Add-a-connection modal |
| Pill button | `.conn-pill` / `.is-honey` / `.is-danger` | Detail-page actions |
| Health pill | `.conn-card-health.is-{ok,warn,err,off,checking}` | With `.conn-health-pulse` for alive states |
| KPI strip | `.conn-card-kpis` + `.conn-kpi` (`.v` / `.l`) | Iowan serif numbers, uppercase labels |
| Multi-shop selector | `.detail-printify-shop-row` + `.conn-select` | Reusable shell — set kind in detail.js |
| Detail page header | `.conn-detail-head` (icon + h1 + role + health pill) | Editorial detail-page chrome |
| Page H1 | `.conn-h1` | 42px, weight 400, italic-accent word |
| Section eyebrow | `.bk-section-eyebrow` | 11px uppercase brand-orange, 0.18em tracking |
| Editorial pull quote | `.bk-pull` | Cream → brand-soft gradient card with serif italic Q |
| Story/script box | `.bk-story-box` | Used for the BrandScript grid |

### Health-pill pulse animation

Two concentric rings radiate outward on a 3.6s loop with a 1.8s phase offset
so one is always blooming while the other has finished. Inner dot has a
synchronized box-shadow halo. Only `is-ok` and `is-checking` pulse — error /
warn / off states stay solid so bad states don't read as friendly motion.

```css
@keyframes conn-health-radiate {
  0%   { transform: scale(0.9); opacity: 0.42; }
  60%  { opacity: 0.06; }
  100% { transform: scale(3.6); opacity: 0; }
}
@keyframes conn-health-breathe {
  0%, 100% { box-shadow: 0 0 0 0 transparent; }
  50%      { box-shadow: 0 0 7px 0 currentColor; }
}
```

Reduced-motion users see a solid dot, no rings (BRAND.md §Motion rules apply).

### Motion tokens

| Token | Value | Use |
|---|---|---|
| Default transition | `160ms ease` | Hover state on cards, tiles, buttons |
| Primary easing | `cubic-bezier(0.16, 1, 0.3, 1)` | Reveals, modals, ring radiate |
| Spring easing | `cubic-bezier(0.34, 1.56, 0.64, 1)` | Chips/badges popping in |
| Pulse loop | `3.6s` | Health-pill radiate + breathe |

### Connector tile icons — real logos

Connector cards/tiles render the platform's real logo on a white tile via
`connections-b2.css` `.conn-*-ic.ic-{kind}` overlays (letter hidden). All
marks live in [`/public/assets/brand-logos/`](public/assets/brand-logos/).
**The connector catalog mirrors the Process & Push pipeline**
(`process-push/src/types/index.ts` `DESTINATIONS`) — only providers the push
pipeline can publish to are offered. Source of truth for the displayed list:
`V1_CATALOG` in `public/connections/connections.js` (+ `CONNECTION_CATALOG`
in `src/connections.ts`).

| Kind | Logo file | Catalog status |
|---|---|---|
| EverBee Research | `everbee-bee.svg` | default (always-on) |
| Brand Kit | gradient mark | default (always-on) |
| OpoShop | `oposhop-icon.png` | available (live) |
| Printify | `printify-icon.svg` | available (live) |
| Etsy | `etsy-logo.svg` | coming soon |
| Shopify | `shopify-icon.svg` | coming soon |
| ShineOn | `shineon-icon.png` | coming soon |
| HelloCustom | `hellocustom-favicon.png` | coming soon |
| Completeful | `completeful-icon.png` | coming soon |
| AnywherePOD | `anywherepod-icon.png` | coming soon |
| Meta Ads | `meta-icon.svg` | coming soon |
| GitHub | `github-icon.svg` | coming soon (dev, non-push) |
| Custom webhook | letter `C` | coming soon (dev, non-push) |
| Ohoney mark | `/assets/brand/ohoney-icon.svg` | — (primary brand asset) |

**Not offered** (kinds retained for safety, but not in the catalog because
they aren't Process & Push destinations): `printful` (`printful.svg`),
`pinterest_ads`. Re-add to `V1_CATALOG` + `CONNECTION_CATALOG` if/when the
pipeline supports them.

### When to use which surface

| Surface | Body class | Treatment |
|---|---|---|
| Marketing pages (`/`, landing, pricing) | `body.landing-dark` | Dark + grain + mesh blobs |
| Workspace app (`/create`, `/admin`) | default `<body>` | Light, flat, no texture |
| **Editorial app surfaces** (`/connections`, `/brand`, `/pipeline-app` redesign) | default `<body>`, page class `.conn-page` or `.bk-page` | **Cream `#fdfaf3`, Iowan serif headings, brand-honey accents, no texture** |

The editorial surface is a third treatment that sits inside the workspace
context (same outer shell, same side-nav) but pulls the surface warmer and
the headings into editorial serif. Use it for pages where context, identity,
and craft matter (Connections, Brand kit, the redesigned Pipeline). Use the
flat light treatment for high-density tool pages (Image Editor, Mockup
Generator).

---

## What's NOT in this file

- Full BrandScript / StoryBrand 7-part structure → [brand-brief.md `messaging:`](brand-brief.md)
- Competitive positioning → [brand-brief.md `positioning:`](brand-brief.md)
- Decision log (why we made each choice) → [brand-brief.md `## Decision Log`](brand-brief.md#decision-log)
- Per-page copy → the page's HTML file (e.g. `public/landing.html`)
- End-user brand kits (the *product feature* for sellers) → `src/brand-kit.ts` — NOT this file

If a question doesn't have an answer here or in `brand-brief.md`, that's a
brand decision waiting to be made. Don't guess — escalate.
