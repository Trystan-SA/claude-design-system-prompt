# Design System Extract: Pull Tokens from Sources

Extract design tokens (color, typography, spacing, radii, shadow) from a brand reference, codebase, or screenshots, and emit a structured tokens file. Use this when starting design work that should match an existing visual language.

A tokens file is the foundation of system thinking. Once tokens exist, future designs reference them — keeping the system consistent without re-asking the user for values every time.

## Phase 1: Identify sources

Determine what to extract from. The user may provide:

- **A codebase** — read theme files (`theme.ts`, `tokens.css`, `_variables.scss`, `tailwind.config.js`, design system source).
- **A live site or screenshots** — extract values from CSS via DevTools-style inspection or by reading screenshots carefully.
- **A brand guide** — PDF, Figma file, or document that lists colors, fonts, spacing.
- **An existing design system project** — a UI kit you can list and read.

If the user hasn't specified, ask. Don't extract from your own assumptions — invented tokens defeat the point.

## Phase 2: Extract by category

Walk through each category. For each, capture concrete values from the source — never guess.

### Colors

Pull:
- **Brand primary** (and its dark/light variants if defined)
- **Brand accent** (and variants)
- **Semantic colors** — success, warning, error, info (and their light backgrounds where defined)
- **Neutral scale** — typically 9–11 steps from near-white to near-black, with a consistent tone (warm / cool / neutral)
- **Surface colors** — background, foreground, card, overlay, border

For each color, record:
- The hex (or oklch) value
- Its name in the source
- Its intended usage (where the source documents it)

Flag inconsistencies — multiple slightly different blues, neutrals on different tones — as a finding for the user. Don't silently merge them; the inconsistency itself is information.

### Typography

Pull:
- **Font families** — sans, serif, mono. Include the full font stack with fallbacks.
- **Font sizes** — the actual scale used (`12 / 14 / 16 / 18 / 20 / 24 / 30 / 36 / 48 / 60` is common but not universal)
- **Font weights** — which weights are actually loaded (don't list weights that aren't deployed)
- **Line heights** — at minimum: tight (~1.1) for headlines, normal (~1.5) for body, loose (~1.7) for long-form
- **Letter spacing** — usually only matters for all-caps labels
- **Text styles** — named combinations (e.g., "Heading 1", "Body Large", "Caption") if the source defines them

### Spacing

Pull the spacing scale used. Common bases: 4px or 8px. The scale typically runs from 0 to 64–128px. Document the actual scale in use, not a generic one.

If the source has separate scales for inset / inline / block / between-components, capture all of them.

### Radii

Pull the corner-radius values used. Typically 3–5 distinct radii (`0`, `4`, `8`, `12`, `9999` for pills).

### Shadows

Pull the shadow system. Typically 3–5 elevations (`shadow-sm` through `shadow-2xl`). Capture the full CSS value (offset, blur, spread, color, opacity).

### Other tokens (if present)

- **Z-index scale** — modals, dropdowns, toasts, tooltips
- **Animation tokens** — duration (`fast`, `normal`, `slow`) and easing curves
- **Breakpoints** — if the system is responsive
- **Container widths** — max-width values for content

## Phase 3: Emit the tokens file

Write a `tokens.css` (or matching format if the source uses a different language: `tokens.ts`, `tokens.json`, etc.). Structure:

```css
:root {
  /* ---------- Colors ---------- */

  /* Brand */
  --color-primary:        #...;
  --color-primary-dark:   #...;
  --color-primary-light:  #...;
  --color-accent:         #...;

  /* Semantic */
  --color-success: #...;
  --color-warning: #...;
  --color-error:   #...;
  --color-info:    #...;

  /* Neutrals */
  --color-gray-50:  #...;
  --color-gray-100: #...;
  /* ... */
  --color-gray-900: #...;

  /* Surfaces */
  --color-bg:      #...;
  --color-surface: #...;
  --color-border:  #...;

  /* ---------- Typography ---------- */

  --font-sans:  "...", -apple-system, sans-serif;
  --font-serif: "...", serif;
  --font-mono:  "...", monospace;

  --text-xs:    12px;
  --text-sm:    14px;
  --text-base:  16px;
  --text-lg:    18px;
  --text-xl:    20px;
  --text-2xl:   24px;
  --text-3xl:   30px;
  --text-4xl:   36px;
  --text-5xl:   48px;

  --weight-regular:  400;
  --weight-medium:   500;
  --weight-semibold: 600;
  --weight-bold:     700;

  --leading-tight:  1.1;
  --leading-normal: 1.5;
  --leading-loose:  1.7;

  /* ---------- Spacing ---------- */

  --space-0:   0;
  --space-1:   4px;
  --space-2:   8px;
  --space-3:  12px;
  --space-4:  16px;
  --space-5:  24px;
  --space-6:  32px;
  --space-7:  40px;
  --space-8:  48px;
  --space-10: 64px;

  /* ---------- Radii ---------- */

  --radius-sm: 4px;
  --radius-md: 8px;
  --radius-lg: 12px;
  --radius-full: 9999px;

  /* ---------- Shadow ---------- */

  --shadow-sm: 0 1px 2px rgba(0, 0, 0, 0.05);
  --shadow-md: 0 4px 6px rgba(0, 0, 0, 0.1);
  --shadow-lg: 0 10px 15px rgba(0, 0, 0, 0.1);
  --shadow-xl: 0 20px 25px rgba(0, 0, 0, 0.15);
}
```

Adapt to the source language and naming convention. If the source uses Tailwind, emit a `tailwind.config.js` extension. If it uses TypeScript, emit a `tokens.ts` with typed exports. Match the project's style.

## Phase 4: Document findings

After emitting the tokens, summarize:

- **Source(s) used** — codebase paths, screenshots, brand guide
- **Categories extracted** — which token sets were found
- **Gaps** — categories where the source didn't define tokens (e.g., no shadow scale documented). These are the user's decisions to make; don't fill them silently.
- **Inconsistencies** — places where the source had near-duplicate values or off-scale outliers. These often represent ad-hoc decisions worth consolidating.
- **Recommended next steps** — typically: review the token file with the user, then use it in subsequent designs.

The output of this skill is a tokens file the user can drop in, plus a clear-eyed report of where the source design system has gaps or inconsistencies.
