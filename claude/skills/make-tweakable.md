# Make Tweakable: Add In-Design Tweak Controls

Add a floating control panel to a finished design that lets the user adjust selected aspects live — colors, fonts, spacing, copy, layout variants, feature flags. Use this when the user wants to "play with options," "see different versions," or compare visual choices side-by-side.

**One file, many variants.** Tweaks let a single design hold multiple visual exploration paths without scattering v1.html / v2.html / v3.html across the project.

## Phase 1: Identify what should be tweakable

Confirm with the user — or propose and check — which aspects to expose. Common candidates:

- **Color** — primary brand color, accent, background tone
- **Typography** — font family, base size, scale ratio
- **Density** — spacing scale (tight / normal / loose)
- **Layout variant** — centered vs left-aligned, single-column vs multi-column
- **Component variants** — button style (filled / ghost / outlined), card treatment
- **Copy** — headline, subhead, CTA text
- **Feature flags** — show/hide testimonials section, show/hide footer signup, etc.

Resist exposing every possible knob. **Keep the tweak surface small** — 3–8 controls is a healthy range. The point is to give the user a few meaningful axes to explore, not to recreate Figma.

If the user didn't ask for tweaks but the design has obvious axes of variation, add 1–2 by default to surface interesting possibilities.

## Phase 2: Design the tweak panel

The tweak panel lives **inside the prototype**, in a floating panel — typically bottom-right corner, semi-transparent, with a subtle border. Title it **"Tweaks"** so the naming matches the toolbar toggle.

Each control should be the right type for the value:

- **Color** → color picker
- **Font / family / variant** → dropdown or button group
- **Number (font size, spacing) → slider** with sensible min/max
- **Boolean (show/hide section) → toggle
- **Copy** → text input or textarea

Keep controls compact. A wide column of tightly stacked controls is better than a sprawling panel.

## Phase 3: Wire up the live updates

Use CSS custom properties for visual tokens — they update everything that references them:

```css
:root {
  --tweak-primary: #0066CC;
  --tweak-font: "Inter", sans-serif;
  --tweak-density: 16px;
}
```

When a tweak changes, update the custom property:

```js
document.documentElement.style.setProperty('--tweak-primary', newColor);
```

For non-CSS values (copy, layout variants, feature flags), use JS state with re-render or DOM manipulation.

## Phase 4: Implement the host protocol

The host environment exposes a toolbar toggle to show/hide the tweak panel. Wire up the protocol so the toggle works:

1. **Register a `message` listener on `window` first** — before announcing availability:
   - `{type: '__activate_edit_mode'}` → show your Tweaks panel
   - `{type: '__deactivate_edit_mode'}` → hide it
2. **Then announce availability:**
   ```js
   window.parent.postMessage({type: '__edit_mode_available'}, '*')
   ```
3. **When a value changes, persist it** by posting back:
   ```js
   window.parent.postMessage({type: '__edit_mode_set_keys', edits: {primaryColor: '#FF6600'}}, '*')
   ```
   You can send partial updates — only the keys you include are merged.

**Order matters:** if you announce `__edit_mode_available` before the listener is registered, the host's activate message lands before your handler exists, and the toggle silently does nothing.

## Phase 5: Persist defaults on disk

Wrap your tweakable defaults in comment markers so the host can rewrite them:

```js
const TWEAK_DEFAULTS = /*EDITMODE-BEGIN*/{
  "primaryColor": "#D97757",
  "fontSize": 16,
  "dark": false
}/*EDITMODE-END*/;
```

The block between markers **must be valid JSON** (double-quoted keys and strings). There must be exactly one such block in the root HTML file, inside an inline `<script>`. The host merges your edits into this block and writes the file back, so changes survive reload.

## Phase 6: Hide the controls when off

The design should look final when Tweaks is toggled off. The panel should be entirely hidden — not just dimmed, not just collapsed to a corner. The user should see the design as a polished artifact with no visible tweak chrome.

This is non-negotiable: any "edit mode UI" left visible when tweaks are off makes the design look unfinished.

## Phase 7: Verify

In the user's preview:

- Toggle the panel on and off via the toolbar — it shows/hides cleanly
- Change each tweak — it updates live
- Reload the page — the tweaked values persist
- Check the design with the panel off — it looks like a finished design, no tweak chrome visible

## Phase 8: Summarize

Report:

- Tweaks exposed and their value types
- Defaults
- Any tweaks you considered but excluded (and why)
- Whether the tweak set covers the user's intended exploration axes
