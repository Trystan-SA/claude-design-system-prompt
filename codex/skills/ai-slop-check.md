# AI Slop Check: Detect and Fix Generic AI Aesthetics

Review the current design for the visual tropes that signal "AI-generated template." Fix any found.

These patterns are rejected because they read as default, not intentional. A design that looks like a hundred other AI outputs is a design that fails to look like the user's design.

Each rule below is **positive-first**: lead with the default to reach for, then list the patterns to detect and replace. The order matters — at write-time you should be biased toward the default; at review-time, scan for the detection patterns.

## Phase 1: Identify the surface to review

Find what to review. In order:

1. The HTML/CSS file the user just edited or asked about.
2. Files modified in the current session.
3. If unclear, ask the user which file or component.

Read the file. Skim referenced CSS, tokens, and component files so you can resolve actual values.

## Phase 2: Single-pass review for AI tropes

Walk through the design and apply each rule below. Single agent — these patterns are obvious enough that parallel dispatch is overkill.

### 1. Gradients — flat or subtle, on-tone

**Default:** flat color from the design system, or a subtle on-tone gradient (two stops, low contrast, same hue family). Flat is almost always stronger.

**Detect & replace:**
- Rainbow / 3+ color gradients (`linear-gradient(135deg, #FF00FF, #00FFFF, #FFFF00)` and similar)
- Saturated purple-to-pink, orange-to-pink, or other "trendy" two-color blends used for hero backgrounds, buttons, or large surfaces
- Gradient overlays on imagery that don't improve legibility or hierarchy

### 2. Emoji — functional or brand-driven only

**Default:** no emoji. Reach for one only if the brand explicitly uses emoji in existing materials, the emoji is functional (a status indicator, a category marker tied to real meaning), or the user asked for them.

**Detect & remove:**
- Emoji prepending headlines, button text, or list items where the brand doesn't use them (`🚀 Get Started`, `✅ Track progress`)
- Repeated emoji used as visual filler (`🎉🎉🎉`)
- Emoji as bullet markers when they don't add meaning

If the layout relied on the emoji for visual weight, replace with a real icon from an established system (Feather, Material, Phosphor, Heroicons) or improve the typographic hierarchy.

### 3. Cards — separate with shadow, thin border, or background

**Default:** distinguish cards with a subtle shadow, a thin all-around border, or pure background separation. Reserve `border-left: 4px solid` for actual semantic emphasis (callouts, alerts, status indicators).

**Detect & replace** the exact pattern:

```css
.card {
  border-radius: 12px;
  border-left: 4px solid #...;
}
```

…used as the *default* card or container style across the design. This combination is so overused it reads as "default SaaS template."

Keep the left border only if it's purposeful (a callout, an alert, a status indicator) and used for that meaning specifically, or it's coming from an existing design system you're matching.

### 4. Imagery — real, licensed, or honest placeholder

**Default, in order of preference:**
- Real photography (Unsplash, brand assets)
- Professional illustration (icon library or commissioned)
- Honest placeholder — striped background with monospace label like `product shot (1200×800)`

A placeholder is better than a bad illustration. It signals "asset needed" without pretending to be the real thing.

**Detect & replace:**
- Custom SVG illustrations of people, scenes, abstract concepts that aren't drawn by a skilled illustrator
- "AI-style" character illustrations (giant heads, flat-color blobs, identical posing)
- Decorative SVG that's clearly placeholder-quality but presented as final

### 5. Type — fonts chosen with intent

**Default:** pick a font with intent, matched to the brand's tone or the medium. If you don't have a brand to draw from, suggest 2–3 alternatives that match the design's tone (geometric, humanist, modern, classical) and let the user pick.

**Detect & question** bare use of:
- Inter
- Roboto
- Arial
- Fraunces
- Bare system stacks (`-apple-system, sans-serif` with no actual font choice)

…used as silent defaults without a brand reason. Keep them only if the brand specifies them, the user asked for them, or they're appropriate for the medium and the user has confirmed. Do not silently swap one generic for another.

### 6. Color — subtly toned whites and blacks

**Default:** use whites and blacks subtly toned to match the palette. Examples:
- Warm: `#FFFAF0` background, `#2D2118` text
- Cool: `#F5F7FA` background, `#1F2937` text
- Neutral: `#FAFAFA` background, `#1A1A1A` text

**Detect & replace:** exact `#FFFFFF` background paired with exact `#000000` text. The combination is harsh, cold, and reads as unfinished.

### 7. Color values — trace to a token or harmonious palette

**Default:** every color value should trace to a design token, brand variable, or `oklch()`-derived harmonious palette. If creating a palette from scratch, use `oklch()` to keep lightness and chroma consistent across hues.

**Detect & consolidate:** color values that don't trace anywhere. Five different blues across the file (`#0066CC`, `#0077DD`, `#3498DB`, `#3B82F6`, `#5B8DEF`) is a smell — colors were invented inline.

### 8. Spacing — snap to a 4px or 8px scale

**Default:** define spacing tokens (`--space-xs: 4px` through `--space-2xl: 64px`) and use them. Multiples of 4 or 8 feel intentional.

**Detect & replace:** off-scale values like `padding: 7px 15px`, `margin: 18px`, `gap: 13px`. They feel chaotic.

## Phase 3: Fix and summarize

Apply fixes directly. For decisions where multiple options are reasonable (e.g., which non-Inter font to use), pick the most defensible default and note the choice in your summary so the user can override.

When done, summarize:
- Tropes found, by category
- Fixes applied
- Open questions for the user (font choice, asset replacement, etc.)
