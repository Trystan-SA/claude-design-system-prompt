# Frontend Aesthetic Direction: Commit to a Look When No Brand Exists

Establish an aesthetic direction (typography, color, density, mood, component style) when the user is designing without an existing brand or design system. Use this **before** drawing hi-fi work in a greenfield context.

**Mocking a hi-fi design from scratch without committing to an aesthetic is the fastest path to AI-template aesthetics.** Without a deliberate direction, you default to safe, generic, indistinct designs. Pick a direction first, then design within it.

## Phase 1: Confirm there's truly no existing context

Before committing to a new direction, double-check that no existing context applies:

- No brand guide
- No existing app or product to match
- No reference site the user explicitly wants to mimic
- No partial design system in the codebase

If any of these exist, **stop and use them** instead. Aesthetic direction is for true greenfield. If the user has a brand and forgot to attach it, ask for it before proceeding.

## Phase 2: Discover the intent

Ask the user (or confirm if they've stated):

- **Three adjectives** that describe the desired feel. ("Editorial / serious / spacious" vs "Playful / bold / loud" vs "Minimal / quiet / utilitarian.")
- **Audience.** B2B engineers respond to different aesthetics than consumer or editorial audiences.
- **Industry context.** SaaS, consumer, editorial, fintech, healthcare, government — each has its own reasonable defaults.
- **Reference designs they admire.** Specific brands, sites, or apps. Ask what specifically they admire — the type, the spacing, the color, the tone, the density?
- **Off-limits.** What aesthetics or tropes does the user explicitly want to avoid?

If the user is unsure, propose 2–3 aesthetic directions framed by adjective and let them pick.

## Phase 3: Commit to the system — make it concrete

Vocalize your decisions as a comment block at the top of the file the user can see. **Be specific.** Vague aesthetic statements ("modern and clean") produce generic designs.

Commit on each axis:

### Typography

Pick **specific** fonts (not "a sans-serif"):

- **Headline font** — name, weight, size scale
- **Body font** — name (often the same family), weight, size scale
- **Mono font** (if needed for code) — name

Avoid the overused defaults — Inter, Roboto, Arial, Fraunces, bare system stacks. Pick something with intent: a humanist sans (Söhne, Suisse), a modern serif (Tiempos, GT Sectra), an editorial classic (Tiempos Headline, Canela), a typewriter mono (JetBrains Mono, IBM Plex Mono), a geometric sans (Söhne Buch, Visby), depending on the mood.

If the user might not have access to a paid foundry, suggest the closest free alternative (e.g., "Inter is overused, but Söhne is paid — try Söhne for production, or Albert Sans / Geist as free alternatives").

Commit to a type scale (sizes, weights, line heights). 1–2 families maximum.

### Color

Pick a tone:

- **Warm** — cream, beige, gold, terracotta, rust
- **Cool** — gray, slate, ice, blue
- **Neutral** — concrete, charcoal, off-white

Then pick:

- **Primary brand color** (with light and dark variants)
- **One accent** (optional — a single accent color is often enough)
- **Semantic colors** (success / warning / error / info)
- **Neutral scale** (5–10 steps from near-white to near-black, on the chosen tone)

Use `oklch()` to keep harmony if the palette is from scratch:

```css
--brand-primary: oklch(55% 0.18 250);
--brand-accent:  oklch(70% 0.15 30);
```

**Subtly tone whites and blacks.** Pure `#FFFFFF` and `#000000` is harsh. Match the chosen tone (e.g., `#FAFAFA` warm-neutral, `#1A1A1A` near-black).

### Density

Pick a spacing scale (4px or 8px base) and commit to a density:

- **Tight** — compact dashboards, dense data UIs (8px multiples, smaller padding)
- **Normal** — typical product UI (8px multiples, comfortable padding)
- **Loose** — editorial, marketing, premium feel (8px multiples, generous padding, lots of whitespace)

The density choice is felt as much as seen — it's a major part of the aesthetic.

### Border radius and shadow

- **Sharp** (radius 0–2px) — utilitarian, brutalist, editorial
- **Soft** (radius 4–8px) — typical modern product
- **Pill / fully-rounded** (radius 9999px on buttons; 12–16px on cards) — playful, friendly, consumer

Shadows similarly: sharp / soft / none. Commit to one elevation system, not a mix.

### Component style

- **Filled** — buttons with solid backgrounds, primary actions saturated
- **Ghost** — buttons with no fill, only border or just text
- **Outlined** — bordered, transparent fill
- **Elevated** — cards float on shadow

Pick a default, with secondary styles for hierarchy.

### Imagery and iconography

- **Photography** — real photos (Unsplash, brand commission, stock)
- **Illustration** — professional library or commission
- **Icons** — Feather, Material, Phosphor, Heroicons, or a paid set
- **Honest placeholders** when assets aren't available

Avoid hand-drawn SVG illustrations.

### Motion

- **Quiet** — minimal motion, transitions only on state changes (200ms ease)
- **Expressive** — entrance animations, scroll-driven reveals, view transitions
- **Playful** — overshoots, springs, micro-interactions on hover

Commit to one mode. Mixed motion modes feel unintentional.

## Phase 4: Document the direction in the file

Write the chosen direction into the file as a visible block — both as a comment at the top of the source AND as a "design system summary" section the user can see in the rendered output. Like a junior designer showing their thinking to their manager.

Example:

```
/* Aesthetic direction:
 * Editorial / serious / spacious.
 * - Type: Tiempos Headline (display) + Söhne (body) — paid foundry.
 *   Free alternative: GT Sectra → Albert Sans.
 * - Color: cool-neutral. #FAFAFA bg / #1A1A1A text.
 *   Brand: oklch(55% 0.18 250) deep blue. No accent.
 * - Density: loose. 8px scale, generous padding.
 * - Radius: 4px (sharp-ish). No shadow — borders only.
 * - Components: ghost buttons. Filled for primary CTA only.
 * - Imagery: real photography, full-bleed.
 * - Motion: quiet. 200ms ease transitions, no entrance animations.
 */
```

## Phase 5: Apply, then test

Build a small surface (a hero, a card, a button group) using the direction. Show it to the user early.

Ask: "Does this read as [the three adjectives you committed to]?" If the answer is no — or if the user pushes back on a specific axis — revise the direction before going broader.

A direction that works at a small scale will hold up across a full design. A direction that doesn't work at a small scale will get worse, not better, as you scale it up.

## Phase 6: Use the direction consistently

Every subsequent design should reference the direction's tokens, not invent new values. If a new design needs a value the direction doesn't define, **add it to the direction first**, then use it. Don't introduce one-off values inline.

Eventually the direction is mature enough to extract into a tokens file — that's when `design-system-extract` becomes useful.

## Phase 7: Summarize

Report:

- The three adjectives
- The committed type, color, density, radius, component, imagery, and motion choices
- Any axes the user should review before you go broader
- The first surface built using the direction (link to the file)
