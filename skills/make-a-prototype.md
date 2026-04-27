# Make a Prototype: Interactive Clickable Prototype

Build a working interactive prototype — clickable, navigable, with real state and feedback. Use this when the user asks for a prototype, mockup, demo, or "make it interactive."

**Prototypes interact.** Static screenshots strung together with `<a>` tags don't count. The point of a prototype is to test the flow with real interaction — clicking, typing, validating, succeeding, failing.

## Phase 1: Discovery

Confirm before building:

- **The flow.** What screens? What's the entry point? What's the goal state? Map it as a list.
- **Fidelity.** Hi-fi (real visuals, real components, real feel) or mid-fi (wireframe-level, focused on flow not polish)?
- **Device frame.** Desktop browser? iOS frame? Android frame? Macos window? Use the appropriate starter component.
- **Variations.** Does the user want one flow or several to compare?
- **Brand / design system.** Always confirm. If none, invoke `frontend-aesthetic-direction` first.
- **Sample data.** What real-looking content fills the screens? Avoid Lorem ipsum.

## Phase 2: Map screens and state

Before building, write down the flow:

```
Screens:
  1. Welcome — "Get started" CTA → goes to 2
  2. Email entry — validate format → goes to 3 on valid, shows error on invalid
  3. Verification — "Check your email" + "Skip" → goes to 4
  4. Profile — name, photo upload → goes to 5
  5. Success — "You're in" + "Get started" → goes to 1 (loop demo)

State:
  - currentScreen: 1
  - email: ""
  - emailError: null
  - name: ""
```

Drop this into the file as a comment block at the top so the user can see your plan.

## Phase 3: Build screen-by-screen

For each screen:

1. **Mount in the DOM** — use display toggling (`display: none` / `display: block`) or React state to switch screens within a single page.
2. **Hi-fi visuals.** Match the design system. Use real components, not generic boxes.
3. **Real content.** Sample data that looks plausible — actual names, actual product copy, actual numbers.
4. **One primary CTA per screen.** Secondary actions are smaller and de-emphasized.

Use the right device frame:

- **iOS** — `copy_starter_component` with `kind: "ios_frame.jsx"`
- **Android** — `copy_starter_component` with `kind: "android_frame.jsx"`
- **macOS window** — `copy_starter_component` with `kind: "macos_window.jsx"`
- **Browser** — `copy_starter_component` with `kind: "browser_window.jsx"`

The frame stays fixed; the prototype lives inside it.

## Phase 4: Wire up interactions

A real prototype has **every interaction wired**, not just the happy path:

- **Navigation.** Clicking the primary CTA moves to the next screen. Back button moves backward. State persists across screens.
- **Form validation.** Empty submission → inline error. Bad format → specific error tied to the field. Valid input → proceed.
- **Loading states.** Async actions (sign-up, save) show a loading indicator. Buttons disable during the request to prevent double-submit.
- **Success feedback.** Toast, inline confirmation, or page transition that confirms the action.
- **Error feedback.** Errors are clear and tied to the field or action that caused them.
- **State changes.** Toggling, selecting, filtering — all update the UI immediately.

If the prototype is a small slice, fake the async work with `setTimeout` to simulate latency. Don't skip the loading state because the work is fake — the loading state is part of what the prototype is testing.

## Phase 5: Wire up sub-state

Many real flows have meaningful sub-state:

- **Selection state** — which item is selected in a list
- **Filter / sort state** — how the data is currently arranged
- **Modal / dropdown state** — open or closed
- **Form state** — values, errors, dirty/pristine

Make these all reactive. If the user clicks a filter chip, the list re-renders. If they open a modal, focus moves to the modal and Escape closes it.

## Phase 6: Persist what matters

Some state should survive a page reload:

- **Current screen** — store in `localStorage`, restore on load
- **Form drafts** — if the user is mid-flow and refreshes, they should pick up where they left off
- **Tweak values** — see `make-tweakable` skill

Refreshing during iterative design is one of the most common user actions. State that doesn't survive reload makes the prototype feel broken.

## Phase 7: Verify

Walk through the full flow in the preview:

- Every CTA leads somewhere
- Every form validates
- Every error is clear and recoverable
- Every async action shows feedback
- Every state change is visible
- Keyboard navigation works (Tab through, Enter to submit, Escape to close modals)
- Focus is visible

If you can't verify a UI behavior, say so explicitly in the summary rather than claiming success.

## Phase 8: Variations (if requested)

If the user asked for variations of the flow, layout, or visual treatment, expose them as:

- **Tweaks** — toggle in a floating panel (see `make-tweakable`)
- **A canvas** — multiple variants side-by-side via the `design_canvas.jsx` starter
- **Toggles in the prototype** — the user clicks between options

Don't scatter v1.html / v2.html / v3.html across the project. One file, many variants.

Summarize briefly: what flows work, what's faked (e.g., "submit calls a setTimeout fake"), what's open for the user to decide.
