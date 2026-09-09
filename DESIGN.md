# DESIGN — 513 Holiday Lighting LLC

Every value in the design system — colors, surfaces, type scale, weights, spacing, radii,
shadows, glows, breakpoints, easing, durations, and the component role aliases — lives in
**`tokens.css`** at the repo root. This document carries only what a token cannot express:
personality, rules of use, behaviors, and anti-patterns. If something here ever states a number or
a color, it is wrong; fix it by deleting it and reading `tokens.css`.

---

## Brand personality

**Warm. Confident. Premium but approachable.**
Feels like a high-end local contractor, not a franchise or a discount coupon site.
The warmth comes from the palette (warm near-black ground, cream, gold that means "lit").
The confidence comes from clean type, generous space, and restraint in decoration.

Gold is the product. It is used only where something is lit: the one primary CTA on a screen, the
anchor card, focus rings, and the success state. Everywhere else gold appears as `--accent-tint`.

---

## Rules of use

- `--text-muted` only on the page ground. Inside any card or lifted surface, use `--text-body`.
- The solid gold gradient is for one primary CTA per screen. Every other gold surface is
  `--accent-tint` with an `--accent-line` border.
- Hairlines and dividers use `--border-*`. Never use a `--surface-*` fill as a border.
- Filled form fields are not "lit": a completed value reads in `--text-high` with a
  `--border-strong` edge, never gold. Gold on a field means focus.
- `--success` is for compact inline confirmations only; the full success panel uses gold at
  scale because that is the one moment the customer is "lit".
- `--warning` exists so that comparison and caution states never borrow the brand gold.

### Do not use
- Blue-black grounds of any kind. Every dark ground is a `--surface-*` token.
- Saturated green as text, and green as a brand accent. The token file has no green.
- Pure white for text or backgrounds. Use `--text-high`.

---

## Typography

One family, Archivo (variable). Display type uses the `--vs-display` variation settings; headings
`--vs-heading`; body `--vs-body`. Eyebrow labels are tracked uppercase (`--ls-eyebrow`) in
`--accent` and always precede the section heading. Body copy respects the `--container-text`
measure. Prices are never a bare fixed number: a "Starting at" label in `--text-muted` caps sits
above the figure.

---

## Motion language

**Principle:** Motion reveals, it does not perform. Every animation serves comprehension or
feedback, not decoration.

- Animate only `transform` and `opacity`. Never `height`, `width`, `top`, `margin`, or `padding`.
- Use the `--dur-*` and `--ease*` tokens. `tokens.css` zeroes the durations under
  `prefers-reduced-motion`; gate any keyframe animation (sparkles, bulb-on, scroll hint) the same
  way, and show reveal targets immediately at full opacity.
- No `will-change` on idle elements. Set it on reveal targets from JS, clear it after the
  animation finishes.
- No choreographed sequences. Each element animates independently.
- Max stagger chain: 3 delays (0, 100ms, 200ms). Do not go deeper.
- Scroll reveals: fade up. Buttons: lift on hover, slight scale-down on press. Cards: lift on
  hover. Gallery items: gentle scale on hover. Sparkles and the scroll hint loop slowly and are the
  first things reduced-motion removes.

---

## Component behaviors

### Buttons
- Primary: the gold gradient role aliases, `--text-on-gold` text, `--glow-gold` on hover lift.
- Ghost: transparent, `--btn-ghost-border`. Hover fills with `--accent-tint` and brightens the
  border to `--accent-line`. Text stays `--text-high`; ghost buttons never turn gold text.
- Active: slight scale-down for tactile feedback.
- Focus: `--focus-ring`. Never suppress the outline.
- Radius is `--radius-md`. Not pill, not square.

### Cards
- `--card-bg`, `--card-border`, `--card-radius`, `--card-shadow`.
- Hover: lift via transform to `--surface-3`. No shadow expansion.
- An anchor card (the one you want chosen) gets `--accent-line` and `--glow-gold`; nothing else
  changes.
- Icon containers: `--accent-tint` fill, `--accent-line` border.

### Forms
- Fields use the `--field-*` roles. Fields sit inside a card, so labels and placeholders are
  `--text-body`, never `--text-muted`.
- Focus: `--field-focus-border` plus `--focus-ring`. Never drop the ring.
- Inline errors use `--error`, `--error-tint`, `--error-border`, with `aria-invalid` and
  `aria-describedby`. Error copy states the fix; never "oops" or "sorry".
- Submitting: `--accent-dim` with `aria-busy`. Disabled: `--btn-primary-disabled`.
- All fields carry `autocomplete` attributes. Inputs use `--fs-body` so iOS does not zoom.
- The general error keeps everything the visitor typed and offers the phone number as a fallback.

### Section labels (eyebrow)
- `--fs-eyebrow`, bold, uppercase, `--ls-eyebrow`, `--accent`. Always precedes the section h2.

---

## Anti-patterns to avoid

- ❌ Any hex or raw color outside `tokens.css`
- ❌ Blue-black backgrounds (conflicts with the warm brand palette)
- ❌ A second solid-gold CTA on the same screen
- ❌ `--text-muted` inside a card
- ❌ A `--surface-*` token used as a border
- ❌ Emoji as permanent UI icons (inconsistent rendering across OS)
- ❌ Invented social proof (reviews, ratings, stats) before they're real
- ❌ AI-generated houses presented as portfolio work
- ❌ More than 3 stagger steps in any reveal group
- ❌ Animating layout properties (height, margin, top, padding)
- ❌ Pure white text or backgrounds
- ❌ Box-shadow expansion on hover for cards (use transform instead)
- ❌ Nested `<nav>` elements (use `<div>` for the mobile dropdown)
