# 513 Holiday Lighting — Higgsfield visual plan and prompt pack (v2)

Rebuilt against tokens.css, the design board, and the quote form.

## What changed from v1

The design board revealed a requirement v1 missed entirely: **four background-removed house renders** — cottage, traditional, large, estate — that sit on the scene with `--glow-gold` supplying the shadow they lose when cut out. That is now the highest-value generation job on this list, ahead of the hero.

Also locked in from the system: architecture is **Cincinnati specifically** (Hyde Park, Mariemont, Mount Lookout are named in the board), not generic Midwest. And the bulb palette has real hexes now.

## Non-negotiables for every generation

**Palette targets.** Everything grades to ink `#0A0907` with `#D9B351` gold. Warm bulbs are `#FFE9C4`. If you use color bulbs, only classic red `#C0472F` and cool white `#BFD4E8` — those three and nothing else. Multicolor rainbow strings are off-system and read cheap.

**Blue hour, never full night.** Deep indigo sky is what the warm bulbs sit against. Full darkness gives them nothing to contrast with and kills the ink-to-gold relationship the whole site runs on.

**Cincinnati architecture.** Brick Colonial Revival, Tudor with steep gables, American foursquare, stone-and-brick center hall. Mature hardwoods, established lots, older streets. Do not let the model default to California stucco, Texas new-build, or English cottage.

**Always append:** `no people, no text, no signage, no logos, no watermarks`.

**Add lens language.** 35mm f/2.0, 85mm f/1.8. It pushes photorealism harder than any adjective.

**Do not generate portfolio content.** The nav has a Gallery item and the form asks customers to send a photo. Those slots take real installs only. AI houses labeled as your work is deceptive advertising, and in a trade sold on "show me a house like mine," it's the one lie that costs you the sale when someone notices.

---

## Job 1 — The four package house renders (do these first)

These get background-removed and composited, so they have different rules from everything else: **isolated subject, flat removable background, no baked ground shadow, and identical camera treatment across all four.** If the angle or scale drifts between them the package row will look broken.

Lock these into every one of the four prompts: three-quarter front view from slightly below eye level, camera at the same distance, house centered and fully in frame with margin on all sides, even blue-hour ambient light, no foreground objects crossing the silhouette.

**1A · Cottage**
> Three-quarter front view of a small one-and-a-half story brick cottage with a steep gabled roof, Cincinnati Tudor influence, warm 2700K incandescent bulbs in an evenly spaced row along every roofline and gable edge, a lit wreath on the door, dusting of snow on the roof, isolated on a flat neutral mid-grey background with no environment and no ground shadow, even ambient blue-hour light, shot on 35mm at f/5.6, sharp throughout, photorealistic architectural render, no people, no text, no signage

**1B · Traditional**
> Three-quarter front view of a two-story red brick Colonial Revival home with symmetrical windows, black shutters, and a centered portico, warm 2700K incandescent bulbs evenly spaced along the rooflines, eaves, and portico edge, snow on the roof, isolated on a flat neutral mid-grey background with no environment and no ground shadow, even ambient blue-hour light, shot on 35mm at f/5.6, sharp throughout, photorealistic architectural render, no people, no text, no signage

**1C · Large**
> Three-quarter front view of a large two-and-a-half story American foursquare home in brick and stone with a wide covered front porch and dormer windows, warm 2700K incandescent bulbs evenly spaced along all rooflines, dormers, porch edge, and porch columns wrapped in warm light, snow on the roof, isolated on a flat neutral mid-grey background with no environment and no ground shadow, even ambient blue-hour light, shot on 35mm at f/5.6, photorealistic architectural render, no people, no text, no signage

**1D · Estate**
> Three-quarter front view of a large multi-gabled stone and brick estate home with multiple roof elevations, a turret, and an attached garage wing, warm 2700K incandescent bulbs evenly spaced along every roofline, gable, dormer, and window frame, columns wrapped in warm light, snow on the roofs, isolated on a flat neutral mid-grey background with no environment and no ground shadow, even ambient blue-hour light, shot on 35mm at f/5.6, photorealistic architectural render, no people, no text, no signage

Generate 6 variations each and pick for **silhouette clarity first** — a clean, cuttable outline beats a prettier house with a messy roofline. Flat mid-grey backgrounds cut better than white or black; white bleeds into snow, black eats the shadow side of the brick.

---

## Job 2 — Hero video (2–3 variations)

Keep the house at middle distance. Motion, snowfall, and shallow depth of field hide the bulb-spacing failures that a static wide shot puts under a magnifying glass. Under 8 seconds, looped, muted, minimal camera movement — fast motion is where AI video falls apart.

**2A · Slow push-in**
> Slow cinematic push-in toward a two-story red brick Colonial Revival home on an established Cincinnati street at blue hour, warm 2700K incandescent bulbs evenly spaced along the rooflines and eaves, warm light spilling from interior windows, fresh snow on the lawn and roof, fine snowfall drifting through frame, bare oak branches framing the edges, deep indigo sky with faint last light at the horizon, shot on 35mm at f/2.0, shallow depth of field, cinematic grade with cool blue shadows and warm highlights, subtle handheld float, no people, no text, no signage

**2B · Lateral drift**
> Slow lateral dolly past a snow-covered front yard at blue hour, a brick Tudor home soft in the background with warm roofline lighting and a lit wreath, foreground evergreen branches passing close to the lens catching warm 2700K light, gentle snowfall, heavy bokeh, 85mm at f/1.8, cinematic winter grade, deep blue ambient with warm accents, no people, no text, no signage

**2C · The safe one — use if A and B fail inspection**
> Extreme close-up of warm incandescent bulbs on a string slowly drifting out of focus into large soft bokeh circles, deep blue-black background, fine snow drifting past, 85mm macro at f/1.4, slow gentle camera drift, warm 2700K glow against cool shadows, cinematic, no people, no text

2C is your insurance. Macro bokeh is the one thing these models do genuinely well, it's honest — it isn't claiming to be a house you lit — and it sits perfectly under "Be the house" in cream Archivo.

Generate 16:9 for desktop and a separate 9:16 for mobile. Do not crop; you lose the composition and the headline safe area.

---

## Job 3 — Atmosphere and texture

**3A · Macro bokeh still** (the workhorse — section backgrounds, CTA bands)
> Extreme close-up of a warm white incandescent bulb in sharp focus, a long string of identical bulbs falling out of focus behind it into large creamy bokeh circles, deep blue-black background, 100mm macro at f/1.8, warm 2700K glow, high contrast between warm light and cool dark, no people, no text

**3B · Abstract light field** (dividers, panel backgrounds)
> Abstract field of large soft warm gold bokeh circles on a deep desaturated warm-black background, out of focus string lights, subtle vertical light streaks, fine film grain, cinematic, no subject, no people, no text

**3C · Snow overlay** (low-opacity layer across dark sections)
> Fine falling snow particles against a solid deep warm-black background, varied particle sizes and depths, soft focus on foreground flakes, subtle film grain, high contrast, no subject, no people, no text

**3D · Roofline detail** (How It Works, process steps)
> Low angle looking up at the eave of a brick home at blue hour, warm incandescent C9 bulbs clipped in an even row along the gutter line, snow resting on the shingles above, deep indigo sky beyond, crisp detail, 35mm at f/4, architectural photography, cinematic cool-warm contrast, no people, no text

**3E · Wrapped tree trunk**
> A mature bare oak trunk wrapped tightly and evenly in warm white string lights in a snowy front yard at blue hour, warm glow pooling on the snow beneath, dark house soft out of focus behind, 50mm at f/2.2, cinematic winter grade, deep blue shadows, no people, no text

**3F · Window glow** (closest match to the aesthetic direction)
> Exterior view of a warmly lit window on a brick home at blue hour, warm interior light glowing through the glass, warm string lights framing the window exterior, frost at the pane corners, snow on the sill, 85mm at f/1.8, shallow depth of field, moody cinematic grade, deep blue-grey exterior against warm interior glow, no people, no text

**3G · Commercial** (for the commercial service split)
> Small-town brick commercial storefront at blue hour with warm white lights outlining the roofline and window frames, snow on the sidewalk, warm light from inside, historic Ohio downtown architecture, empty street, 35mm, cinematic desaturated grade, no people, no readable text or signage

---

## Placement

| Asset | Where |
|---|---|
| 1A–1D house renders | Package cards — cottage on Roofline, traditional on Full Facade, large and estate on Estate. `--glow-gold` on the container supplies the missing shadow. |
| 2A or 2B | Desktop hero behind the near-black inset panel |
| 2C | Mobile hero, or fallback poster loop |
| 3A macro bokeh | Behind service tiles, heavily darkened |
| 3B light field | Section dividers, CTA band |
| 3C snow | Low-opacity overlay across dark sections |
| 3D, 3E, 3F | How It Works steps, About |
| 3G | Commercial split |
| — | **Gallery, testimonials, before/after: real installs only** |

---

## Post

Grade all of it to one palette before it ships: crush blacks toward `#0A0907`, hold light sources genuinely warm near `#FFE9C4`, keep saturation down everywhere else. Ten images that agree with each other beat one perfect image sitting next to nine that don't.

Judge everything at full size. Bulb spacing and roofline geometry are where the failures live, and they are invisible in a thumbnail. If a shot is nearly right but the bulbs wander, darken and blur that region rather than regenerating — behind a scrim at hero scale, nobody sees it.
