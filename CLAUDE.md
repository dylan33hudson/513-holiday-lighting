# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this is

A single-page static marketing site for **513 Holiday Lighting LLC**, a Cincinnati Christmas-light
installation company. The entire site is one file: `index.html` (HTML + inline `<style>` + inline
`<script>`, no framework, no build step, no dependencies besides two Google Fonts loaded via CDN link).

There is no package.json, build tool, linter, or test suite. "Development" means editing
`index.html` directly and viewing it in a browser (`open index.html`).

## Required reading before editing

- **`PRODUCT.md`** — business context, target audience, the persuasion role of each page section,
  and hard content constraints (e.g. do not invent testimonials/stats/reviews; keep existing copy
  verbatim unless fixing grammar; stats bar and gallery are intentional placeholders until real
  data exists).
- **`DESIGN.md`** — the full design system: color tokens, type scale, motion/easing rules, spacing,
  component patterns, and an explicit anti-patterns list. Any visual change should match tokens
  already defined in `:root` inside `index.html` rather than introducing new ad-hoc values.

Treat these two files as the spec. If a requested change conflicts with them (e.g. adding fake
reviews, using pure white, animating `height`/`margin`), flag the conflict rather than silently
complying.

## Architecture of index.html

Single file, four parts in order:

1. **`<head>`** — meta/SEO tags, Open Graph tags, and a JSON-LD `LocalBusiness` schema block.
   Several values are unresolved placeholders marked `<!-- REPLACE: ... -->` (canonical URL,
   og:image URL, schema `url`) — do not fill these with invented domains.
2. **`<style>`** — design tokens on `:root` (colors, easing, durations, radii, fonts) followed by
   reset, type scale, layout, buttons, nav, then per-section styles in the same order the sections
   appear in the body. Section-specific CSS lives next to its section's styles, not centralized.
3. **`<body>`** — nav, then sections in this fixed order (each has an `id` used for nav anchors):
   hero → `#services` → `#how-it-works` → `#gallery` → `#why-us` → `#testimonials` →
   `#service-area` → `#quote` → cta-banner → footer. Section order encodes the persuasion funnel
   described in `PRODUCT.md`; don't reorder without checking that doc.
4. **`<script>`** (bottom of file, single inline block) — footer year, sticky-nav scroll class,
   mobile menu toggle, decorative hero "sparkles" generation (skipped under
   `prefers-reduced-motion`), and an `IntersectionObserver`-based scroll-reveal system that toggles
   `.in` on elements with class `.reveal` and manages `will-change` manually.

## Known placeholders that still need real values

Search for `REPLACE` in `index.html` to find all of them. Currently:
- Canonical URL / OG image URL / schema `url` (head) — no real domain yet.
- Hero photo, gallery photos, team photo — currently placeholder blocks, need real `<img>` tags.
- Formspree form action (`action="https://formspree.io/f/YOUR_FORM_ID"`) — needs a real endpoint ID.
- Testimonials — placeholder reviews, must be swapped for real ones (never fabricated).
- Service area city list — verify against actual coverage before shipping.
- Social links (Facebook/Instagram) — currently unset.

## Design/motion constraints worth remembering while editing

- Only animate `transform` and `opacity`; never `height`, `width`, `top`, or `margin`.
- Respect `prefers-reduced-motion` (already wired up for sparkles/reveals — extend the same pattern
  for any new motion).
- Max 3 stagger steps (0, 100ms, 200ms) in any reveal group.
- No pure white (`#FFFFFF`) or blue-black — use the warm palette tokens in `:root`.
- No emoji as permanent UI icons; use inline SVG (see existing buttons/icons for the pattern).
- Mobile nav dropdown must stay a `<div>`, not a nested `<nav>`.
