# Component Extract: Identify Reusable Components from a Design

Walk a design and identify the reusable components hidden inside it. Emit a component inventory the user can extract into a real component library or design system. Use this when the user has a finished page or flow and wants to "make it a system," "build a component library," or hand off a structured set of pieces.

**Pages are arrangements of components.** A design without identified components is a pile of one-offs. Extracting components turns the design into something maintainable.

## Phase 1: Identify the surface

Determine what to walk:

- A single hi-fi design file
- A multi-page flow
- A whole project of designs

Read all relevant files. Build a mental model of the visual vocabulary in use.

## Phase 2: Walk the design and inventory

Walk the design surface section by section. For each visual element, ask:

1. **Does this exact pattern appear more than once?** (Same button on three pages → component candidate.)
2. **Could this pattern reasonably appear elsewhere?** (Even if it's only in one place now, would it likely repeat? E.g., a card style, a form input, a header.)
3. **Does it have variants?** (A button has primary, secondary, ghost variants. A card has with-image and without-image variants.)
4. **Does it have states?** (Hover, active, disabled, focus, loading.)

If yes to any, it's a component candidate.

Group findings into the standard component categories:

### Foundational

- **Color tokens** — brand, semantic, neutral
- **Spacing tokens** — the spacing scale in use
- **Type tokens** — font families, sizes, weights, line heights
- **Radius tokens** — corner-radius scale
- **Shadow tokens** — elevation scale
- **Motion tokens** — transition durations and easing

(See `design-system-extract` for token-level detail. This skill builds on that.)

### Atoms

- **Button** — variants (primary, secondary, ghost, destructive); sizes; with/without icon; states
- **Input** — text, email, password, number, search; with/without label; with/without error
- **Checkbox / radio / toggle**
- **Select / dropdown**
- **Tag / chip / badge**
- **Avatar**
- **Icon** — list of icon sizes and the icon set in use
- **Link** — inline link, standalone link

### Molecules

- **Form field** — label + input + helper + error
- **Card** — variants (with image, with footer, minimal); states (hover, selected)
- **Toast / alert** — variants (info, success, warning, error)
- **Modal / dialog**
- **Dropdown menu**
- **Tooltip**
- **Pagination control**

### Organisms

- **Header / nav bar**
- **Footer**
- **Sidebar nav**
- **Tab group**
- **Table / data grid**
- **Form** (composite of fields + submit + validation pattern)
- **Hero section**
- **Feature grid**
- **Empty state**

### Templates / page-level

- Landing page template
- Detail page template
- List/index template
- Empty state page

## Phase 3: For each component, document

For every component you identified, capture:

- **Name** — short, conventional, imperative-noun (e.g., `Button`, `EmptyState`, `FormField`)
- **Purpose** — one-sentence description of when to use it
- **Variants** — the named visual or behavioral variations
- **Sizes** — if size variants exist
- **States** — default, hover, active, focus, disabled, loading (whichever apply)
- **Tokens used** — which color, spacing, type tokens it references
- **Composition** — what other components it's built from (e.g., `Card` uses `Button`)
- **Accessibility notes** — keyboard support, ARIA, contrast considerations
- **Do / Don't** — at least one short do and one don't (e.g., "Don't stack two primary buttons in a row")

Format as a structured doc — a component inventory the user can hand to a developer or use as the basis for building a component library.

## Phase 4: Identify the gaps

While walking, you'll find:

- **Inconsistencies** — three slightly-different button styles where one should serve. Flag them and recommend a canonical version.
- **Missing states** — a component with a hover state but no focus state, or no disabled state. Flag the gap.
- **Missing variants** — a component the user might reasonably need but doesn't yet exist (e.g., destructive button variant on a design with delete actions but only primary buttons).
- **Off-scale values** — components that use spacing or sizes outside the established token scale. Flag and snap.

These gaps are part of the deliverable — they're the work needed to turn the design into a real system.

## Phase 5: Emit the inventory

Write the inventory to a file (e.g., `component-inventory.md`) with one section per component, structured as above. If the user wants the components built as actual code, follow up with the build work — but the inventory file is the primary output of this skill.

For visual reference, optionally generate a "component library" page that renders each component with its variants and states. Use the `design_canvas.jsx` starter if you want a grid layout.

## Phase 6: Recommend next steps

After the inventory, suggest:

- **Extract tokens** (`design-system-extract`) if not already done
- **Build the component library as code** if the user wants it as a real artifact
- **`Polish-pass`** on each component to make sure they hold up at the atomic level
- **`Make tweakable`** on the component library so the user can adjust the system live

## Phase 7: Summarize

Report:

- Number of components inventoried (by category — atom / molecule / organism)
- Inconsistencies and gaps flagged
- Output file path
- Recommended next step
