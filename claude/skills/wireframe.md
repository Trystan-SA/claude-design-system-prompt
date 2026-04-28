# Wireframe: Explore Many Ideas Quickly

Produce low-fidelity wireframes or storyboards to explore a flow, layout, or idea before committing to hi-fi design. Use this when the user wants to "explore options," "sketch something out," "see a few directions," or when the design problem is open enough that hi-fi work would be wasted at this stage.

**Wireframes are disposable.** They exist to test ideas, not to be polished. Their value is in the breadth of options, not the fidelity of any one.

## Phase 1: Understand the goal

Confirm:

- **What's being explored.** A single screen, a multi-screen flow, a navigation pattern, an information hierarchy, an interaction model?
- **The user goal.** What is the imagined user trying to accomplish on this screen / flow?
- **Constraints.** Mobile or desktop? Existing context or greenfield? Any non-negotiable elements (logo position, mandatory legal copy, fixed brand color)?
- **Number of variations.** 3 minimum. 5–6 is a healthy ceiling for one round.
- **Axis of variation.** What dimension should the variations differ on? (Layout? Information density? Step count in the flow? Where the primary CTA lives? Single-page vs multi-page?)

If the user just says "wireframe a sign-up flow" without specifying, propose 2–3 axes (e.g., "single-page form vs multi-step wizard vs progressive disclosure") and ask which they want explored.

## Phase 2: Establish wireframe conventions

Wireframes have a visual language. Stick to it so the user reads the wireframes as wireframes — not as broken hi-fi.

Conventions:

- **Greyscale only.** No brand color. Black, white, and 2–3 grays.
- **System sans-serif.** No type personality. The user shouldn't form opinions about the font yet.
- **Boxes for content areas.** A rectangle labeled "headline" or "image" or "feature card."
- **Striped placeholders for imagery.** Use the diagonal-stripe pattern with a monospace label (`product shot 1200×800`). Never an actual image — that pulls focus.
- **Lorem ipsum or skeleton copy.** Don't write final copy at this stage. Use ipsum, or short label-style placeholders ("Headline goes here / one short sentence about the value prop").
- **Annotations are welcome.** Numbered callouts pointing to key decisions are fine — the wireframe is a thinking artifact.

This is the one context where hand-drawn-feeling SVG (rectangles, lines, simple icons) is acceptable — because everything is at the same low fidelity.

## Phase 3: Sketch variations

Produce **at least 3** variations. Each one should differ on the axis you established in Phase 1.

For a single screen, lay out the variations side-by-side using the `design_canvas.jsx` starter component. For a multi-screen flow, build each variation as a small storyboard (3–5 screens stacked or arranged horizontally).

Vary across:

- **Layout** — centered single-column vs left-aligned vs split-screen vs grid
- **Information density** — minimal hero vs feature-rich vs feed-style
- **Flow structure** — single page vs multi-step vs progressive disclosure
- **Primary CTA placement** — top, bottom, sticky, inline
- **Navigation pattern** — top nav, side nav, bottom tab, hamburger

Start with the most by-the-book variation (the obvious one) and end with the most novel (the riskier bet). The user is more likely to pick something interesting if they see the safe option next to a riskier one.

## Phase 4: Annotate the variations

For each variation, add 2–4 annotation points so the user can see what's interesting about it:

```
- Variation 1 (single-column wizard):
    → simple, focused, but slow
- Variation 2 (single-page form):
    → fastest path, but feels heavy on first impression
- Variation 3 (progressive disclosure):
    → balances both, but requires more JS state
```

Place annotations next to each variation, not in a separate doc. The user should be able to read the variation and the rationale together.

## Phase 5: Capture decisions

After the user picks a direction, capture what was decided:

- The chosen variation (or hybrid)
- What attracted them to it
- What they explicitly rejected from the other options
- Any new constraints surfaced during the review

This becomes the brief for the hi-fi follow-up.

## Phase 6: Hand off

Wireframes are a stepping stone. When the user has picked a direction, suggest one of:

- **`make-a-prototype`** to take the chosen wireframe to hi-fi interactive
- **`make-a-deck`** if the wireframe was for a presentation
- A new round of wireframes if the user wants to iterate further at low fidelity

Do not invest hi-fi polish in the wireframes themselves. They've served their purpose; let them go.

## Phase 7: Summarize

Report:

- Number of variations produced
- Axis of variation
- Recommended next step
- Any open questions the wireframe round surfaced
