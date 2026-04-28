# Make a Deck: Slide Presentation in HTML

Build a slide presentation as a single HTML file with fixed-size slides that letterbox to any viewport. Use this when the user asks for a deck, presentation, slides, or pitch.

A deck is fixed-size content (typically 1920×1080, 16:9) that scales to fit any screen. Don't hand-roll the scaling — use the deck shell starter.

## Phase 1: Discovery

Confirm before building:

- **Audience.** Engineers? Executives? Customers? Internal team? The audience determines tone and density.
- **Format.** Aspect ratio (16:9 default, 4:3 occasionally). Slide count (most decks land at 8–15).
- **Length / time budget.** A 10-minute deck is ~10 slides. A 30-minute deck is ~20–25.
- **Tone.** Formal corporate, casual internal, marketing-bold, technical-detail.
- **Source content.** Is there a PRD, doc, or existing material to work from? Read it before sketching.
- **Speaker notes.** Off by default. Only add when explicitly requested.
- **Brand / design system.** Always confirm. If none, invoke the `frontend-aesthetic-direction` skill before drawing.

If the user gave enough context to skip the question round (e.g., "make a 5-slide deck for engineering all-hands from this PRD"), proceed.

## Phase 2: Plan the layout system

Before building any slide, commit to a layout system. Vocalize this in the file as a comment block at the top so the user can see your plan.

A typical deck has 4–6 layout types:

- **Cover / title slide** — large title, optional subtitle, brand mark, date
- **Section header** — full-bleed background color or image, large section title
- **Content slide** — headline + supporting visuals (chart, image, or bullet list)
- **Quote / pull-out** — large quote, attribution, lots of breathing room
- **Comparison / two-column** — side-by-side content
- **Closing / CTA** — final ask, contact info, next steps

For each layout, decide:

- Background color or image style
- Headline size and position
- Body content area
- Footer treatment (page number, brand mark, none)

Limit yourself to **1–2 background colors** across the deck. Section headers may break to a third color, but no more.

## Phase 3: Build the deck shell

Use the deck-shell starter component (`copy_starter_component` with `kind: "deck_stage.js"`). It handles:

- Fixed-size scaling and letterboxing
- Keyboard and tap navigation
- Slide-count overlay
- localStorage persistence (slide index)
- Print-to-PDF
- `data-screen-label` and `data-om-validate` tagging

Each slide is a direct child `<section>` of the `<deck-stage>` element.

Add `data-screen-label` attributes to each slide so the user can reference them by name when commenting:

```html
<section data-screen-label="01 Title">...</section>
<section data-screen-label="02 Agenda">...</section>
```

**Slide labels are 1-indexed** to match the slide counter the user sees.

## Phase 4: Build slide-by-slide

Build one slide at a time, in order. Show the user the file as soon as you have 1–2 slides — don't perfect 15 slides in private and then reveal.

For each slide:

- **Type rules.** Body text never smaller than 24px on a 1920×1080 canvas; ideally 32px+. Headlines 60–96px+.
- **Hierarchy.** One primary message per slide. Supporting elements smaller, more muted.
- **Imagery.** When the slide is text-heavy, commit to imagery from the design system, or use honest placeholders (striped backgrounds with monospace labels). Don't pad with hand-drawn SVG illustrations.
- **No filler.** "Why choose us?" / "About this deck" / generic fluff slides cost the user attention. Cut them.
- **Charts and data.** Show what matters. Cut columns and data points that don't support the slide's point.

Use the spacing and color tokens from the design system (or the aesthetic established in Phase 2). Don't introduce new values inline.

## Phase 5: Speaker notes (only if requested)

Speaker notes go off by default. Only add them when the user explicitly asks. When they do:

- Add a `<script type="application/json" id="speaker-notes">` array in the head, one entry per slide
- Use full conversational scripts, not bullet outlines
- Slides with speaker notes can carry less on-screen text — the speaker fills in the gaps

The deck shell renders speaker notes automatically when present.

## Phase 6: Verify and deliver

Walk the deck top to bottom in the user's preview. Check:

- Scaling works at multiple viewport sizes
- Slide counter increments correctly
- Keyboard nav (arrows, space) works
- No content overflows the slide bounds
- Type sizes meet the minimums (24px+ body)
- Color contrast meets WCAG (run quick contrast check, or invoke `accessibility-audit` for thoroughness)

For end-of-turn delivery, surface the final HTML file and run a verification pass yourself — render it headlessly (Playwright or chrome-devtools) and check scaling, layout, and overflow. Codex doesn't have a verifier subagent; you do this in-loop.

Summarize briefly: caveats (e.g., placeholder imagery still needed), next steps (e.g., real charts to swap in), and any decisions the user should sign off on.
