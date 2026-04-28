# AI Slop Check: Detect and Fix Generic AI Aesthetics

Review the current design for the visual tropes that signal "AI-generated template." Fix any found.

These patterns are rejected because they read as default, not intentional. A design that looks like a hundred other AI outputs is a design that fails to look like the user's design.

## Phase 1: Identify the surface to review

Find what to review. In order:

1. The HTML/CSS file the user just edited or asked about.
2. Files modified in the current session.
3. If unclear, ask the user which file or component.

Read the file. Skim referenced CSS, tokens, and component files so you can resolve actual values.

## Phase 2: Single-pass review for AI tropes

Walk through the design and flag every instance of the following. Single agent — these patterns are obvious enough that parallel dispatch is overkill.

### 1. Aggressive gradients

Flag:
- Rainbow / 3+ color gradients (`linear-gradient(135deg, #FF00FF, #00FFFF, #FFFF00)` and similar)
- Saturated purple-to-pink, orange-to-pink, or other "trendy" two-color blends used for hero backgrounds, buttons, or large surfaces
- Gradient overlays on imagery that don't improve legibility or hierarchy

Fix: replace with flat color from the design system or a subtle, on-tone gradient (two stops, low contrast, same hue family). Flat is almost always stronger.

### 2. Emoji as decoration

Flag:
- Emoji prepending headlines, button text, or list items where the brand doesn't use emoji (`🚀 Get Started`, `✅ Track progress`)
- Repeated emoji used as visual filler (`🎉🎉🎉`)
- Emoji as bullet markers when they don't add meaning

Keep emoji only if:
- The brand explicitly uses them in their existing materials
- The emoji is functional (a status indicator, a category marker tied to real meaning)
- The user asked for them

Fix: remove the emoji. If the layout relied on the emoji for visual weight, replace with a real icon from an established system (Feather, Material, Phosphor, Heroicons) or improve the typographic hierarchy.

### 3. Rounded corners with left-border accent

Flag the exact pattern:

```css
.card {
  border-radius: 12px;
  border-left: 4px solid #...;
}
```

Used as the *default* card or container style across the design. This combination is so overused it reads as "default SaaS template."

Keep only if:
- The left border is purposeful (a callout, an alert, a status indicator) and used for that meaning specifically
- It's coming from an existing design system you're matching

Fix: drop the left border for default cards. Use a subtle shadow, a thin all-around border, or just background separation. Reserve `border-left` for actual semantic emphasis.

### 4. Hand-drawn SVG illustrations

Flag:
- Custom SVG illustrations of people, scenes, abstract concepts that aren't drawn by a skilled illustrator
- "AI-style" character illustrations (giant heads, flat-color blobs, identical posing)
- Decorative SVG that's clearly placeholder-quality but presented as final

Fix: replace with one of:
- Real photography (Unsplash, brand assets)
- Professional illustration (icon library or commissioned)
- Honest placeholder — striped background with monospace label like `product shot (1200×800)`

A placeholder is better than a bad illustration. It signals "asset needed" without pretending to be the real thing.

### 5. Overused fonts as defaults

Flag bare use of:
- Inter
- Roboto
- Arial
- Fraunces
- Bare system stacks (`-apple-system, sans-serif` with no actual font choice)

Used as defaults without a brand reason.

Keep if:
- The brand specifies them
- The user asked for them
- They're appropriate for the medium and the user has confirmed

Fix: pick a font with intent. If you don't have a brand to draw from, suggest 2–3 alternatives that match the design's tone (geometric, humanist, modern, classical) and let the user pick. Do not silently swap to another generic.

### 6. Pure white and pure black

Flag exact `#FFFFFF` background paired with exact `#000000` text. This combination is harsh, cold, and reads as unfinished.

Fix: subtly tone both. Examples:
- Warm: `#FFFAF0` background, `#2D2118` text
- Cool: `#F5F7FA` background, `#1F2937` text
- Neutral: `#FAFAFA` background, `#1A1A1A` text

Pick a tone consistent with the rest of the palette.

### 7. Random invented colors

Flag color values that don't trace to a token, brand variable, or harmonious palette. Five different blues across the file (`#0066CC`, `#0077DD`, `#3498DB`, `#3B82F6`, `#5B8DEF`) is a smell — it means colors were invented inline.

Fix: consolidate to a single token. If creating a palette from scratch, use `oklch()` to keep lightness and chroma consistent across hues.

### 8. Random spacing values

Flag `padding: 7px 15px`, `margin: 18px`, `gap: 13px`, and other off-scale values. They feel chaotic.

Fix: snap to a 4px or 8px scale. Define spacing tokens (`--space-xs: 4px` through `--space-2xl: 64px`) and use them.

## Phase 3: Fix and summarize

Apply fixes directly. For decisions where multiple options are reasonable (e.g., which non-Inter font to use), pick the most defensible default and note the choice in your summary so the user can override.

When done, summarize:
- Tropes found, by category
- Fixes applied
- Open questions for the user (font choice, asset replacement, etc.)
