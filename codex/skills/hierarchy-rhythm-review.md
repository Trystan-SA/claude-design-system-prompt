# Hierarchy and Rhythm Review

Review the current design for visual hierarchy and rhythm — the two qualities that most distinguish "intentional" from "AI-generated." Fix issues found.

**Hierarchy guides the eye:** what gets looked at first, second, third.
**Rhythm makes the design feel intentional:** repetition with strategic variation.

When hierarchy and rhythm are right, the design feels effortless to scan. When they're wrong, even well-intentioned content feels confusing or boring.

## Phase 1: Identify the surface

Find what to review. In order:

1. The HTML/CSS file the user just edited or asked about.
2. The most recently modified design file in the session.
3. If unclear, ask.

Read the file and the styles it references. Note the medium (slide / page / mobile / dashboard) — hierarchy and rhythm rules vary by context.

## Phase 2: Run two review passes

Codex runs as a single agent loop. Run both passes **sequentially** against the file, collecting findings as you go before fixing.

### Pass 1: Hierarchy review

For every screen, slide, or major section:

1. **Identify the primary, secondary, and tertiary elements.** What is the user supposed to look at first? Second? Third? If you can't tell, the hierarchy is broken.

2. **Check size differentiation.** Headings should be visibly larger than body text. The primary CTA should be larger than secondary actions. Flag cases where similar content is at very different sizes (inconsistent), and cases where different-importance content is at similar sizes (flat hierarchy).

3. **Check color hierarchy.** Primary actions should be in a saturated brand color. Secondary actions in neutral. Disabled or de-emphasized content in light gray. Flag cases where everything is the same color (no signal) or where unimportant elements are in the brightest color (wrong signal).

4. **Check weight hierarchy.** Headlines bold, body regular, captions regular-and-light. Flag everything-bold (nothing stands out) or everything-regular (no emphasis).

5. **Check position.** In left-to-right languages, eyes start at top-left. The most important content (logo, primary headline, primary CTA) should be in the prime real estate. Flag layouts where the primary element is buried in the bottom-right.

6. **Check density signals.** Loose spacing around important elements signals "pay attention." Tight spacing signals "supporting." Flag cases where the most important content is crammed and unimportant content has lots of breathing room — that's reversed.

7. **Verify "the 5-second test."** A first-time user should understand what to look at and what to do within 5 seconds. If you can't, the eye doesn't have a clear path through the design.

### Pass 2: Rhythm review

For the document as a whole:

1. **Check the spacing scale.** All padding, margin, and gap values should snap to a consistent scale (typically multiples of 4px or 8px). Flag every random value (`padding: 7px`, `margin: 18px`, `gap: 13px`). List the spacing scale that's been *implicitly* used and identify outliers.

2. **Check the type scale.** Every font size should come from a defined scale. Flag arbitrary sizes (`font-size: 17px` or `font-size: 23px` when the rest of the design uses 16/20/24).

3. **Check repetition.** Sections that should look like each other (cards in a grid, list items, feature blocks) should share padding, gap, font sizes, and structure. Flag near-duplicates that are subtly different — either they should be identical or they should be deliberately different.

4. **Check strategic variation.** A long page or deck should break its pattern occasionally — a different background color, a wider section, a centered CTA — to create rhythm. Flag pages that are completely uniform (monotonous) and pages that vary every section (chaotic).

5. **Check color palette discipline.** The design should use 3–5 colors (plus their tints/shades) across all elements. Flag cases where 8+ distinct colors appear, or where slightly different blues/grays are used in different places.

6. **Check section structure.** Sections should be visually distinguishable (background change, divider, padding shift) but follow a consistent pattern. Flag sections with no visual separation (where content blurs together) and sections with too many separation styles (no rhythm).

7. **Check alignment.** Elements should align to a grid. Flag elements that are off by a few pixels in a way that suggests inconsistent margins rather than intentional offset.

## Phase 3: Aggregate and fix

Wait for both agents. Aggregate findings.

For each issue:

- **Random spacing → snap to scale.** If the file already has a scale, snap to the nearest value. If it doesn't, define one (typically 4px or 8px multiples) and update all spacing.
- **Random font sizes → snap to type scale.** Same approach.
- **Flat hierarchy → introduce contrast.** Make headlines bigger, primary CTAs more prominent, body text consistently neutral.
- **Reversed hierarchy → swap signals.** If the unimportant element is brightest, mute it. If the important element is buried, reposition.
- **Monotony → introduce a strategic break.** Change the background of one section, increase the padding of the CTA section, vary the layout of one card.
- **Chaos → consolidate.** Pick the strongest pattern and make others match it.

Apply fixes directly. For ambiguous cases, lean toward the more aggressive hierarchy — a too-strong hierarchy is easier to dial back than a too-weak one to dial up.

## Phase 4: Summarize

Report:
- Hierarchy issues found and fixed
- Rhythm issues found and fixed
- Any judgment calls that the user should review (e.g., "I made the CTA significantly larger — adjust if too aggressive")
- Open recommendations (e.g., "Consider committing to a strict 8px spacing scale; current file has both 4px and 8px increments mixed")
