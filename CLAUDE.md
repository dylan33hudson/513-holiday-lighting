# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A single-page static marketing site for **513 Holiday Lighting LLC**, a Cincinnati Christmas-light
installation company. No framework, no build step, no package manager. The page is `index.html`
(HTML + inline `<style>` + inline `<script>`), which imports one stylesheet: `tokens.css` at the
repo root. One Google Font (Archivo, variable) is loaded via CDN link. The site deploys to Netlify
(`netlify.toml`, publish directory `.`) and the quote form uses Netlify Forms.

"Development" means editing those files directly and viewing in a browser (`open index.html`).

## The one rule that governs everything else

**`tokens.css` at the repo root is the only source of truth for design values.**

- Every color, type size, line height, letter spacing, weight, spacing step, radius, shadow, glow,
  container width, breakpoint number, easing, and duration is defined there and nowhere else.
- **No hex value, and no raw `rgb()`/`rgba()`/`hsl()` color, may appear anywhere except
  `tokens.css`.** In `index.html`, `styles/hero.css`, and any future file, colors are `var(--…)`.
  If you need an alpha variant of a token, use `color-mix(in srgb, var(--token) N%, transparent)`.
  If a value genuinely doesn't exist yet, add it to `tokens.css` first, then reference it.
- The old `:root` block in `index.html` and the color, type, radius, and motion tables that used to
  live in `DESIGN.md` are superseded and have been removed. Do not reintroduce either.
- Pure black `rgba(0,0,0,…)` inside `box-shadow` is the only tolerated raw color, and only because
  the `--shadow-*` tokens use it. Prefer the `--shadow-*` tokens.

Three usage rules that tokens alone can't enforce:

1. **`--text-muted` only on the page ground (`--surface-0`).** Inside a card or any surface above
   `--surface-0`, labels, captions, and placeholders use `--text-body`. (`--text-muted` misses AA
   on `--surface-2`.)
2. **The solid gold gradient (`--btn-primary-bg-top` → `--btn-primary-bg-bottom`) is reserved for
   one primary CTA per screen.** Every other gold surface (tags, badges, hover fills, anchor cards)
   uses `--accent-tint`, with `--accent-line` for its border.
3. **Hairlines and dividers use the `--border-*` tokens, never `--surface-3`.** A surface is a
   fill; a border is a border.

## Required reading before editing

- **`tokens.css`** — the design system. Read the section comments; they carry the contrast notes.
- **`PRODUCT.md`** — business context, target audience, the persuasion role of each section, and
  hard content constraints (never invent testimonials, stats, or reviews; gallery and stats are
  honest placeholders until real data exists).
- **`DESIGN.md`** — brand personality, motion rules, component behaviors, and anti-patterns. It no
  longer carries values; anything numeric or color-related lives in `tokens.css`.

If a requested change conflicts with these files (fake reviews, pure white, a new hex value,
animating `height`/`margin`), flag the conflict rather than silently complying.

## Architecture of index.html

1. **`<head>`** — meta/SEO, Open Graph + Twitter card, favicons, JSON-LD `LocalBusiness` schema,
   the Archivo font link, hero preload, then `tokens.css`. The canonical URL and the absolute
   og:image URL still need the live domain; do not fill them with invented domains. The one raw
   color in the file is `<meta name="theme-color">`, which mirrors `--surface-0` because a meta
   tag cannot read CSS variables.
2. **`<style>`** — reset, type, layout, buttons, nav, then per-section styles in body order. No
   `:root` block; section CSS references `var(--…)` from `tokens.css`.
3. **`<body>`** — fixed nav + mobile menu `<div>`, then `<main>`: hero (`#top`) → proof strip →
   `#services` → `#how-it-works` → photo band → `#pricing` → `#details` → `#products` → `#gallery` →
   `#why-us` (with the promise grid) → `#about` → `#service-area` → `#quote` → CTA band → footer.
4. **`<script>`** — footer year, sticky-nav scroll class, mobile menu toggle, an
   `IntersectionObserver` scroll-reveal that toggles `.in` on `.reveal` elements and manages
   `will-change` manually, and the quote form's photo preview + async POST to Netlify Forms with
   inline success and error states. Hero motion (rise, hairline draw, parallax) is pure CSS.

## Assets

- `assets/logo-cream-lockup.png` — nav mark. `logo-gold-lockup.png`, `mark-cream-512.png`,
  `mark-gold-512.png` are alternates.
- `assets/hero-graded.jpg` — hero photo (the CSS bokeh gradient in `.hero__bokeh` paints behind it
  as the fallback). `assets/products/*.jpg` — the four product photos.
- `assets/og-image.jpg`, `favicon-32.png`, `apple-touch-icon.png`, `icon-512.png` — referenced from
  `<head>`.
- `docs/513-holiday-lighting-hero.png` and `docs/product-originals/` are the full-size originals.
  Reference only; the shipped JPEGs are derived from them.
- `docs/archive/` holds old hero explorations. Not a spec; do not build from them.
- `513 Pricing and Quote Form (standalone).html` is the design-canvas export the quote section was
  built from. Reference only.

## Known placeholders that still need real values

Search for `REPLACE` in `index.html`. Also:
- Canonical URL and absolute og:image URL once the domain exists.
- Testimonials and gallery — real installs only; the gallery ships as an honest empty state until
  the first 2026 installs go up in November.
- Service-area city list — verify against actual coverage.
- Social links (Facebook/Instagram) — unset.
- Founders photo in `#about` — a marked placeholder until it exists.

## Motion and markup constraints

- Only animate `transform` and `opacity`; never `height`, `width`, `top`, or `margin`.
- Respect `prefers-reduced-motion`. `tokens.css` zeroes the `--dur-*` tokens under it; gate any
  keyframe animation the same way.
- Max 3 stagger steps (0, 100ms, 200ms) in any reveal group.
- No pure white and no blue-black. Every dark ground is a `--surface-*` token.
- No emoji as permanent UI icons; use inline SVG.
- The mobile nav dropdown must stay a `<div>`, not a nested `<nav>`.
