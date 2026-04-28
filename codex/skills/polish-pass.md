# Polish Pass: End-of-Design Quality Gate

Run a comprehensive quality check before a design is shown to stakeholders or shipped. **A polished design and an unpolished design are the same idea executed at different levels of care — and the gap is what people actually see.**

This skill is the umbrella for the four narrower review skills. Use it as the final gate before delivery.

## Phase 1: Confirm scope

Determine what to polish:

1. The HTML file the user just finished or asked about.
2. The current main deliverable in the project.
3. If unclear, ask.

Read the file. Take note of:
- The medium (slide / page / mobile / dashboard / animation)
- The deployment context (internal review / customer-facing / marketing)
- Any user-stated constraints or scope boundaries

If the design is clearly mid-flight (broken layout, missing sections, placeholder content the user is still iterating on), say so and ask whether they really want a polish pass now or after the structure is settled.

## Phase 2: Run four review passes

Codex runs as a single agent loop, so run the four reviews **sequentially** against the file, collecting findings as you go. Each pass is the equivalent of one of the standalone review skills, scoped to this file. Do not stop after the first issue — complete all four passes before fixing, so the fix phase has the full picture.

### Pass 1: Accessibility audit

Run the full `accessibility-audit` review:
- Contrast and color (WCAG AA minimums, color-only signaling, problematic combinations, pure white/black flags)
- Semantic HTML and structure (headings, button vs div, labels, alt text, ARIA discipline)
- Keyboard navigation and focus (reachability, tab order, visible focus, skip links)
- Motion, forms, and miscellany (`prefers-reduced-motion`, flash limits, error specificity, hit-target size)

Report findings as a categorized list.

### Pass 2: AI slop check

Run the full `ai-slop-check` review:
- Aggressive gradients
- Emoji-as-decoration
- Rounded corners with left-border accent (used as default)
- Hand-drawn SVG illustrations
- Overused fonts as defaults (Inter, Roboto, Arial, Fraunces, bare system stacks)
- Pure white and pure black
- Random invented colors
- Random spacing values

Report findings.

### Pass 3: Hierarchy and rhythm review

Run the full `hierarchy-rhythm-review`:
- **Hierarchy:** primary/secondary/tertiary differentiation, size, color, weight, position, density, 5-second test
- **Rhythm:** spacing scale discipline, type scale discipline, repetition, strategic variation, color palette discipline, section structure, alignment

Report findings.

### Pass 4: Interaction states pass

Run the full `interaction-states-pass`:
- Inventory of interactive elements
- For each: default, hover, active, disabled, focus, loading
- Transitions (0.15–0.3s for state changes, longer for entry/exit, `prefers-reduced-motion` respected)
- Feedback for actions (success/error confirmation, state visibility)

Report findings.

## Phase 3: Aggregate, deduplicate, prioritize

Wait for all four agents. Aggregate findings into one list.

**Deduplicate.** If two agents flagged the same issue (e.g., "focus ring removed" appears in both accessibility and interaction-states), merge into one entry.

**Prioritize.** Group findings into:

1. **Blockers** — accessibility failures (contrast under WCAG, missing keyboard support, removed focus rings, missing labels). These break the design for real users; fix all of them.
2. **Quality issues** — AI slop tropes, broken hierarchy, missing interaction states. These cheapen the design; fix all of them.
3. **Polish recommendations** — subtler improvements (suggested color tone shift, spacing-scale tightening). Apply when in scope; flag when out of scope.

## Phase 4: Fix

Fix every blocker and every quality issue directly. Apply polish recommendations when they don't conflict with the user's stated direction.

For ambiguous fixes (e.g., "the design uses Inter but the user hasn't given a brand font preference"), pick a defensible default and note the choice in the summary so the user can override.

For findings that are clearly false positives or outside scope (e.g., "the third-party embed has low contrast — but it's a third-party widget"), note them and skip.

## Phase 5: Re-verify

After fixes, do a quick re-check on the high-risk areas:
- Did the contrast fixes maintain the visual style, or did they wash out a brand color?
- Did the focus ring additions overlap with neighboring content?
- Did the hierarchy adjustments make the primary CTA actually feel primary?

If anything looks off, fix it. If you're unsure, flag it for the user's review.

## Phase 6: Final summary

Report concisely:

- **Verdict** — "Ready to ship" / "Ready after user reviews flagged decisions" / "Needs more iteration before polish makes sense"
- **Blockers fixed** — count by category (accessibility / AI slop / hierarchy / interaction)
- **Polish applied** — count by category
- **Open decisions** — judgment calls the user should sign off on (font choice, color tone shift, hierarchy emphasis level)
- **Out of scope** — anything you noticed but didn't touch (e.g., copy edits, content additions, new features)

Keep the summary short. The user can ask for detail if they want it. **Brief summaries — caveats and next steps only.**
