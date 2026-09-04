# DESIGN — 513 Holiday Lighting LLC

## Brand personality

**Warm. Confident. Premium but approachable.**
Feels like a high-end local contractor, not a franchise or a discount coupon site.
The warmth comes from the palette (amber gold, dark brown-black, cream white).
The confidence comes from clean type, generous space, and restraint in decoration.

---

## Color system

All values verified for WCAG AA contrast.

| Token | Hex | Role |
|-------|-----|------|
| `--bg-deep` | `#0A0806` | Page base, hero |
| `--bg-mid` | `#100D0A` | Alternate sections |
| `--bg-section` | `#140F0C` | Gallery, area |
| `--bg-card` | `#1A1410` | Cards, stats bar |
| `--green` | `#1A5C3A` | Brand accent (logo) |
| `--green-lt` | `#237A4E` | Step connector |
| `--gold` | `#C8A44A` | Primary accent: CTAs, labels, icons |
| `--gold-lt` | `#E2C068` | Hero italic, gold highlights |
| `--gold-dim` | `rgba(200,164,74,.14)` | Icon backgrounds, subtle fills |
| `--warm-white` | `#FFF6E0` | Headings, primary text |
| `--text` | `#A89880` | Body text (7.3:1 on `--bg-deep`) |
| `--text-lt` | `#D4C8B4` | Subheadings, important body (12+:1) |
| `--text-muted` | `#8A7864` | Gallery notes, form notes, fine print (5.1:1 — AA ✓) |
| `--border` | `rgba(200,164,74,.12)` | Card edges, dividers |

### Contrast summary (WCAG AA = 4.5:1 for text, 3:1 for UI)
- `--text` on `--bg-deep`: ~7.3:1 ✓
- `--text-lt` on `--bg-deep`: ~12:1 ✓
- `--text-muted` on `--bg-mid`: ~5.1:1 ✓
- `--gold` on `--bg-deep`: ~8.8:1 ✓
- `#06090F` on `--gold` (button text): ~8.8:1 ✓
- `--warm-white` on `--bg-deep`: ~18:1 ✓

### Do not use
- Blue-black (#06090F, #0A0F1A) — reserved for old revisions only
- Saturated green as text — it fails contrast on dark bg
- Pure white (#FFFFFF) — too stark; use `--warm-white` instead

---

## Typography

**Fonts:** Playfair Display (serif, headings) + Inter (sans, body/UI)

### Type scale

| Role | Size | Weight | Font |
|------|------|--------|------|
| Hero display | `clamp(3.2rem, 8vw, 7rem)` | 700 | Playfair Display |
| Section h2 | `clamp(2rem, 4vw, 3.2rem)` | 700 | Playfair Display |
| Card h3 | `clamp(1.15rem, 2vw, 1.45rem)` | 500 | Playfair Display |
| Eyebrow label | `0.72rem` | 600 | Inter, uppercase, 0.2em tracking |
| Body (card) | `0.95rem` | 400 | Inter |
| Body (UI small) | `0.88rem` | 400 | Inter |
| Fine print | `0.78rem` | 400 | Inter |

### Rhythm rules
- Section headings: `line-height: 1.1`
- H3 cards: `line-height: 1.25` (needs room to breathe at smaller sizes)
- Body copy: `line-height: 1.7`
- Labels / UI text: `line-height: 1.4`
- Max line length: 65ch for body, 45ch for hero sub

---

## Motion language

**Principle:** Motion reveals, it does not perform. Every animation serves comprehension or
feedback — not decoration.

### Easing tokens

| Token | Value | Use |
|-------|-------|-----|
| `--ease-out` | `cubic-bezier(0.22, 1, 0.36, 1)` | Scroll reveals, entrances |
| `--ease-ui` | `cubic-bezier(0.4, 0, 0.2, 1)` | Hover states, nav, buttons |

### Duration scale

| Token | Value | Use |
|-------|-------|-----|
| `--dur-fast` | `160ms` | Button active press, quick feedback |
| `--dur-mid` | `280ms` | Hover transitions |
| `--dur-reveal` | `580ms` | Scroll reveal entries |

### What moves and how

| Element | Property | Duration | Easing |
|---------|----------|----------|--------|
| Scroll reveal | `opacity` 0→1, `translateY` 24px→0 | 580ms | `--ease-out` |
| Stagger delay | +100ms per child | — | — |
| Button hover | `translateY` 0→-2px | 280ms | `--ease-ui` |
| Button active | `scale` 1→0.97, `translateY` -2px→0 | 160ms | `--ease-ui` |
| Nav link | `color` | 280ms | `--ease-ui` |
| Service card hover | `translateY` 0→-4px, `::before` opacity | 280ms | `--ease-ui` |
| Gallery hover | `scale` 1→1.04 | 400ms | `--ease-ui` |
| Sparkle | `opacity` + `scale` | 2–5s | `ease-in-out` (infinite) |
| Scroll hint | `translateY` | 2.2s | `ease-in-out` (infinite) |
| Nav scroll in | `background`, `padding`, `box-shadow` | 280ms | `--ease-ui` |

### Rules
- Animate only `transform` and `opacity` (never `height`, `width`, `top`, `margin`)
- No `will-change` on idle elements — set on reveal targets via JS, clear after animation
- `prefers-reduced-motion`: collapse all durations to 0.01ms, disable sparkles, disable
  scroll hint animation. Reveal elements show immediately at full opacity.
- No choreographed sequences. Each element animates independently.
- Max stagger chain: 3 delays (0, 100ms, 200ms). Do not go deeper.

---

## Spacing

Section vertical padding: `clamp(5rem, 10vw, 8rem)` top and bottom.
Container width: `min(1200px, 90vw)`.
Card internal padding: `2.75rem 2.25rem` (generous, premium feel).
Gap between cards: `1px` (divider approach) or `1.5rem` (open grid approach).

---

## Component patterns

### Buttons
- Primary: gold gradient, dark text. Hover: lift + glow shadow.
- Ghost: transparent, white border. Hover: gold border + gold text.
- Active: slight scale-down (0.97) for tactile feedback.
- All: 6px border-radius (not pill, not square — purposeful).

### Cards
- Background: `--bg-card`. Border: 1px `--border`.
- Hover: darker bg + gold top-rule via `::before`. No box-shadow expansion.
- Icon container: gold-dim fill, gold-dim border, 12px radius.

### Forms
- Input bg: `rgba(255,255,255,.04)` — subtle depth against dark bg.
- Focus: gold border + gold ring shadow. No outline suppression.
- All fields use `autocomplete` attributes for mobile usability.

### Section labels (eyebrow)
- 0.72rem, Inter 600, ALL CAPS, 0.2em tracking, gold color.
- Always precedes the section h2.

---

## Anti-patterns to avoid

- ❌ Blue-black backgrounds (conflicts with warm brand palette)
- ❌ Emoji as permanent UI icons (inconsistent rendering across OS)
- ❌ Invented social proof (reviews, ratings, stats) before they're real
- ❌ More than 3 stagger steps in any reveal group
- ❌ Animating layout properties (height, margin, top)
- ❌ Pure white text or backgrounds
- ❌ Box-shadow on hover for cards (use transform instead)
- ❌ Nested `<nav>` elements (use `<div>` for the mobile dropdown)
