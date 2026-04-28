# Accessibility Audit: WCAG and Inclusive Design Review

Review the current design for accessibility issues across contrast, semantic structure, keyboard navigation, motion, and forms. Fix any issues found. **Good accessibility is good design — it benefits everyone.**

## Phase 1: Identify the surface to audit

Determine what to review. In order of preference:

1. The HTML file the user just edited or asked about.
2. The most recently modified design file in the project.
3. If unclear, ask the user which file to audit.

Read the file end-to-end. Note: the framework or component library in use, the deployed accessibility level expected (WCAG AA is the standard default), and any user-stated constraints.

## Phase 2: Run four review passes

Codex runs as a single agent loop, so run the four reviews **sequentially** against the file, collecting findings as you go. Do not stop after the first issue — complete all four passes before fixing.

### Pass 1: Contrast and Color

For each text and UI element:

1. **Verify text contrast.** Normal text (under 18px) needs 4.5:1; large text (18px+ bold or 24px+) needs 3:1; UI components (buttons, icons, focus rings) need 3:1. Compute the actual ratio for any color pair you can resolve (resolved hex values, tokens followed back to their source). Flag every failing pair with the ratio and the required minimum.
2. **Check for color-only signaling.** Flag any state communicated by color alone — green/red without an icon, blue link with no underline, chart with no legend or text labels.
3. **Check for difficult color combinations.** Red+green (most common colorblindness), blue+yellow at similar lightness, light gray on white, colored text on colored backgrounds with similar brightness.
4. **Check whites and blacks.** Flag pure `#FFFFFF` on `#000000`. Subtly toned (e.g., `#FAFAFA` / `#1A1A1A`) is preferred — though this is style, not WCAG, so flag as a recommendation.

### Pass 2: Semantic HTML and Structure

For the document structure:

1. **Heading hierarchy.** Exactly one `<h1>`. No skipped levels (don't go from `<h2>` to `<h4>`). Headings describe content, not styled visual size.
2. **Right element for the role.** `<button>` not `<div onclick>`. `<a href>` not `<div>` styled as a link. `<label for="id">` linked to `<input id="id">`. `<nav>`, `<main>`, `<article>`, `<section>`, `<aside>` for landmarks.
3. **Alt text on every meaningful image.** Decorative images use `alt=""` so screen readers skip them. Meaningful images describe what they convey, not what they are (`alt="Wireless headphones, side view"` not `alt="product"`).
4. **Form input labels.** Every input has an associated `<label>` (or `aria-label` if visually labelless). Placeholder text alone is not a label — placeholders disappear when the user types.
5. **Avoid ARIA when semantic HTML works.** Flag `role="button"` on a `<div>` if it could just be a `<button>`. ARIA is a patch, not a default.

### Pass 3: Keyboard Navigation and Focus

For every interactive element:

1. **Keyboard reachable.** Everything clickable must also be reachable with Tab. Hover-only menus, modals that don't open with keyboard, dropdowns that need mouse hover all fail.
2. **Logical tab order.** The Tab sequence should follow reading order (top to bottom, left to right). Flag explicit `tabindex` values greater than 0 (they distort the natural order).
3. **Keyboard interaction patterns.** Modals close on Escape. Dropdowns open with Enter/Space and navigate with arrows. Forms submit on Enter from a field.
4. **Visible focus rings.** Flag any `outline: none` without a replacement. The replacement should be visible and meet 3:1 contrast against the adjacent background. `:focus-visible` is preferred over `:focus`.
5. **Skip links.** For pages with significant repeated navigation, recommend a "Skip to main content" link as the first focusable element.

### Pass 4: Motion, Forms, and Misc

1. **`prefers-reduced-motion` respected.** Animations and transitions over a couple hundred milliseconds should have a `@media (prefers-reduced-motion: reduce)` block that shortens or removes them.
2. **No flashing content.** Anything flashing more than 3 times per second can trigger photosensitive epilepsy. Auto-playing videos, strobe effects, rapid loops — flag and require pause control.
3. **Form errors.** Every error message is specific ("Email address is invalid" not "Invalid"), tied to its field (visually adjacent and via `aria-describedby`), and announced to screen readers.
4. **Required fields.** Marked with text and/or icon plus the `required` attribute, not color alone.
5. **Input types and autocomplete.** `<input type="email">` for email, `type="tel"` for phone, `autocomplete` attributes for autofill. These improve mobile keyboard UX and accessibility.
6. **Hit-target size.** Buttons, links, and tappable areas should be at least 44px × 44px on touch surfaces.

## Phase 3: Aggregate and fix

Aggregate findings from all four passes into a single list, deduplicating where multiple passes flagged the same issue.

Fix each issue directly. For ambiguous cases (e.g., "this contrast is 4.4:1, very close to passing"), apply the fix anyway — accessibility is the floor, not the ceiling.

If a finding is a clear false positive or out-of-scope (e.g., a third-party embed you can't modify), note it and skip it. Don't argue with the finding — just move on.

When done, summarize:
- Issues found by category (contrast / semantic / keyboard / motion-forms)
- Issues fixed
- Any issues left for the user (third-party content, ambiguous cases, design decisions outside accessibility)
