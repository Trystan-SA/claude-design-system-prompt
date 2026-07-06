# Polish Pass: End-of-Design Quality Gate

Run a comprehensive quality check before a design is shown to stakeholders or shipped. **A polished and an unpolished design are the same idea executed at different levels of care — and the gap is what people actually see.** This is the umbrella for the four narrower review skills; use it as the final gate before delivery.

## Phase 1: Confirm scope

Polish the HTML file the user just finished or asked about; otherwise the project's main deliverable; if unclear, ask. Read it and note the medium (slide / page / mobile / dashboard), the deployment context (internal / customer-facing / marketing), and any stated constraints.

If the design is clearly mid-flight (broken layout, missing sections, placeholder content still being iterated), say so and ask whether to polish now or after the structure settles.

## Phase 2: Run four review passes

Codex runs as a single agent loop, so run the four reviews **sequentially** against the file, collecting findings as you go. Each pass is the equivalent of one standalone review skill, scoped to this file. Do not stop after the first issue — complete all four passes before fixing, so the fix phase has the full picture.

1. **Accessibility audit** (`accessibility-audit`): contrast and color (WCAG AA minimums, color-only signaling, pure white/black); semantic HTML and structure (headings, button vs div, labels, alt text, ARIA discipline); keyboard navigation and focus (reachability, tab order, visible focus); motion, forms, and hit-target size.
2. **AI slop check** (`ai-slop-check`): aggressive gradients; emoji decoration; default left-border cards; hand-drawn SVG; overused default fonts (Inter, Roboto, Arial, Fraunces, bare system stacks); pure white/black; invented colors; off-scale spacing.
3. **Hierarchy and rhythm review** (`hierarchy-rhythm-review`): primary/secondary/tertiary differentiation via size, color, weight, position, density, and the 5-second test; spacing and type scale discipline, repetition, strategic variation, palette discipline, section structure, alignment.
4. **Interaction states pass** (`interaction-states-pass`): per-element default/hover/active/disabled/focus/loading; transition timing (0.15–0.3s state changes, longer entry/exit); `prefers-reduced-motion`; action feedback and state visibility.

## Phase 3: Aggregate, deduplicate, prioritize

Aggregate findings from all four passes into one list. Merge duplicates (e.g., "focus ring removed" from both accessibility and interaction-states). Group into:

1. **Blockers** — accessibility failures (contrast under WCAG, missing keyboard support, removed focus rings, missing labels). These break the design for real users; fix all.
2. **Quality issues** — AI slop tropes, broken hierarchy, missing interaction states. These cheapen the design; fix all.
3. **Polish recommendations** — subtler improvements (color tone shift, spacing-scale tightening). Apply when in scope; flag when out.

## Phase 4: Fix and re-verify

Fix every blocker and quality issue directly. For ambiguous fixes (e.g., the design uses Inter but no brand font is stated), pick a defensible default and note it so the user can override. Note and skip clear false positives (e.g., a third-party embed's contrast).

Then re-check the high-risk areas: did contrast fixes wash out a brand color? Do the new focus rings overlap neighboring content? Does the primary CTA now actually feel primary? Fix what looks off; flag what you're unsure about.

## Phase 5: Final summary

Report concisely — the user can ask for detail:

- **Verdict** — "Ready to ship" / "Ready after user reviews flagged decisions" / "Needs more iteration before polish makes sense"
- **Blockers fixed and polish applied** — counts by category
- **Open decisions** — judgment calls to sign off (font choice, color tone shift, emphasis level)
- **Out of scope** — noticed but untouched (copy edits, content additions, new features)
