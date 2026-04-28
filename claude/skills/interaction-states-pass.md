# Interaction States Pass

Verify every interactive element has a complete set of states (default, hover, active, disabled, focus) plus appropriate transitions and feedback. Add what's missing.

**Interactive elements without state feedback feel broken.** A button without a hover state looks like a label. A disabled button that looks enabled feels broken when nothing happens on click. A removed focus ring locks out keyboard users.

This skill is the safety net before a design is shown to users.

## Phase 1: Identify interactive elements

Walk the design and inventory every interactive element. The categories:

- **Buttons** — `<button>`, anything `role="button"`, anything that calls a click handler
- **Links** — `<a>`, anything that navigates or opens external content
- **Form inputs** — `<input>`, `<textarea>`, `<select>`, file pickers, range sliders, color pickers
- **Toggles** — checkboxes, radios, custom switches
- **Cards or rows that act as links** — clickable rows in a table, clickable cards in a grid
- **Navigation items** — tabs, sidebar links, breadcrumbs
- **Custom widgets** — dropdowns, accordions, modals, popovers

For each element, you need to verify the full state set in Phase 2.

## Phase 2: Per-element state verification

For each interactive element, check all six aspects below.

### 1. Default (resting) state

The element looks clearly interactive at rest:
- Buttons have background fill, border, or both — distinct from body text
- Links are obviously links — color + underline, or a clear visual treatment
- Form inputs have visible borders or fills

Flag elements that look like static text and only reveal interactivity on hover. Some users will never hover (touch devices, keyboard users).

### 2. Hover state

Visual change on cursor over. At minimum a color shift. Better: color + shadow + slight transform (e.g., `translateY(-2px)`).

Flag missing hover states. Don't use opacity reduction as the hover state for buttons — it makes them look disabled.

### 3. Active / pressed state

Visual change while clicking — typically a darker color, a slight scale-down (`transform: scale(0.98)`), or a return-to-baseline if the hover lifted the element. The active state confirms to the user that the click registered before the action completes.

### 4. Disabled state

Clearly disabled: lower opacity (~0.6), no hover effect, `cursor: not-allowed`, neutral or muted color. The disabled state must look different from both the default and the hover states.

If a button is disabled because the user hasn't met some condition (e.g., "fill all required fields"), provide an indicator of *why* — a tooltip, an inline message, or a `title` attribute. A silently disabled button is a frustration trap.

### 5. Focus state

Visible focus ring for keyboard users. Use `:focus-visible` over `:focus` so the ring shows for keyboard navigation but not on every mouse click.

Required:
- The ring is visible against the adjacent background (3:1 contrast minimum)
- The ring is at least 2px thick, with 2px offset
- `outline: none` is **never** used without a replacement

### 6. Loading state (for elements that trigger async work)

For buttons that submit forms, save data, or otherwise wait on a network call:
- Disable the button immediately on click (prevent double-submission)
- Replace the label with a spinner or "Loading…" text
- Re-enable and restore the label on completion

For elements that fetch data on render: a skeleton, spinner, or progress indicator while waiting.

## Phase 3: Verify transitions

Every state change should be smoothly transitioned, not snapped:

```css
button {
  transition: background 0.2s ease, transform 0.2s ease, box-shadow 0.2s ease;
}
```

Check transition durations:
- **0.15–0.3s** for state changes (hover, focus, active) — feels responsive
- **0.3–0.5s** for entry/exit (modals, drawers, toasts) — feels composed
- **Avoid** transitions slower than 0.5s for micro-interactions; they feel laggy
- **Avoid** transitions of 0s or no transition; state changes feel broken

Wrap motion-heavy transitions in `@media (prefers-reduced-motion: reduce)` to shorten or remove for users who prefer reduced motion.

## Phase 4: Verify feedback for actions

For every action the user takes, the result should be visible:

- **Form submission success** — toast, inline message, or page redirect with confirmation
- **Form submission failure** — clear error message, tied to the field if field-specific
- **Validation errors** — appear when the field loses focus or on submit; cleared when the user fixes the issue
- **State changes (toggle on/off, item added to a list)** — immediate visual change, optionally with a brief animation

Flag silent successes ("user submitted, page does nothing visible") and silent failures ("user submitted, nothing happened, no error shown") — both feel broken.

For state visibility:
- The current page or tab in navigation is visually distinct
- Selected items in a list are visually distinct
- Active filters or sorts are visually distinct

## Phase 5: Apply fixes

For each missing state or feedback element, add it. Use the design system's tokens for colors and timings. If the design system doesn't define something, use sensible defaults:

- Hover: 10–15% darker than the default (or `color-mix` if the design uses modern CSS)
- Active: another 10% darker, or `transform: scale(0.98)`
- Disabled: opacity 0.6 + `cursor: not-allowed`
- Focus: `outline: 2px solid var(--color-primary); outline-offset: 2px`
- Transition: `0.2s ease`

For elements where the right state isn't obvious (e.g., a toggle button — what's the active vs. inactive vs. hover-on-active state?), make a judgment call and note it in the summary.

## Phase 6: Summarize

Report:
- Interactive elements inventoried
- Missing states added (counts by category — hover / active / disabled / focus / loading)
- Transitions added or normalized
- Feedback added (toasts, error messages, loading indicators)
- Any judgment calls the user should review
