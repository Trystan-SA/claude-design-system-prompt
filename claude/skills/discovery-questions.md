# Discovery Questions: Kickoff Question Protocol

Run a structured question round at the start of new or ambiguous design work. Use this whenever the user asks for something new and you don't already have what you need to start. **Asking good questions is the single biggest lever for design quality.** Bad designs come from missing context, not missing skill.

## Phase 1: Read what's already attached

Before asking anything, **read every attached resource** the user has provided:

- Codebases or files
- Screenshots
- Brand guides or PDFs
- Linked design system or UI kit projects
- The user's stated brief

Your questions should be informed by what's already there. Asking "do you have a brand guide?" when they just attached one is the fastest way to lose the user's confidence.

## Phase 2: Decide whether to ask

**Ask when:**

- The work is new or ambiguous
- The output, audience, or fidelity are unclear
- You don't know which design system, UI kit, or brand is in play
- The user hasn't specified how many variations they want
- The task spans multiple non-trivial dimensions (audience + format + tone + content all unspecified)

**Skip asking when:**

- The user gave you everything you need
- It's a small tweak or follow-up to existing work
- The user is explicit about scope, audience, and constraints
- The task is "recreate this exact thing" (a clear reference)

If you're not sure whether to ask: ask.

## Phase 3: Build the question set

Every question round should include the following **always-ask** questions, plus at least 4 problem-specific questions.

### Always-ask: design context

- **Starting point.** "Is there a UI kit, design system, codebase, brand guide, or screenshots I should match? If not, I'll need to commit to an aesthetic from scratch — confirm if that's OK."
- This question is non-negotiable. Starting a hi-fi design without context produces bad design. Confirm via a question, not in your own assumptions.

### Always-ask: variations

- **How many variations of the overall design?** (1, 2, 3, more)
- **What axes should I vary on?** (Visual, layout, interaction, copy, tone)
- **Variations of specific elements?** ("How many variations of the hero?" "Of the CTA button?")

### Always-ask: novelty

- **By-the-book or novel?** "Do you want options that match existing patterns, novel/creative ideas, or a mix?"

### Always-ask: tweaks

- **What should be tweakable in the final design?** (Colors, copy, layout, components — what does the user want to be able to adjust live?)

### Always-ask: focus axis

- **What do you care about most — flows, copy, or visuals?** This tells you where to spend exploration effort.

### Problem-specific (4+)

These vary by the task. Examples:

**For a deck:**
- Audience and audience knowledge level?
- Time budget / slide count?
- Tone (formal corporate, casual internal, marketing-bold)?
- Speaker notes needed?
- Existing source material to work from?

**For a landing page:**
- What action do you want users to take?
- Who is the primary persona?
- What competitors or references inspire you (positively or negatively)?
- Mobile-first or desktop-first?

**For an interactive prototype:**
- What flow / what screens?
- Hi-fi or mid-fi?
- Device frame?
- What's the goal state of the flow?
- Sample data — what real-looking content fills the screens?

**For a brand or aesthetic:**
- Mood / tone in 3 adjectives?
- Existing brands or designs you admire (and what specifically about them)?
- Anything explicitly off-limits?
- Industry / context (B2B SaaS, consumer, editorial, government)?

Aim for **at least 10 questions total** when the brief is genuinely ambiguous. Fewer if the user has given a lot of context already.

## Phase 4: Format the question round

Use the `questions_v2` tool when starting something new or ambiguous. It renders native form components and the user answers in a structured way.

For each question:

- **Prefer multiple choice** (radio or checkbox) when possible — easier for the user than open-ended text
- **Always include "Explore a few options" and "Decide for me"** as choices on multiple-choice questions — these are escape hatches the user often wants
- **Include "Other"** for open-ended fallback
- **Use SVG options** for visual choices (layout style, icon style, color swatch, mood)
- **Use sliders** for numeric ranges with sensible bounds — be generous, users want to go further than expected
- **Use file-pickers** for "attach an asset"
- **Use freeform** for genuinely open-ended questions

Order the questions so the most important ones come first — the form streams in, and the user can start answering before the rest finishes loading.

Keep titles short. Subtitles are optional clarifications.

## Phase 5: End the turn

`questions_v2` does not return an answer immediately. After calling it, **end your turn** to let the user answer. Do not try to anticipate answers and proceed before they respond.

When the user submits answers, they come back as a structured object. Read every answer before starting to design.

## Phase 6: Confirm and proceed

Once the user has answered:

- Briefly recap the choices that will most affect the design ("OK — landing page, B2B audience, formal tone, three variations on different visual treatments, single CTA, no novel ideas")
- Note any answers that surprised you or that you'd push back on (gently — the user is the manager)
- Then proceed to the appropriate building skill (`make-a-deck`, `make-a-prototype`, `wireframe`, etc.)

## Phase 7: Re-question on signal change

If during the design work you discover that an early answer was wrong (e.g., the user said "no novel ideas" but their feedback shows they actually want bolder choices), re-question. Don't carry on with the wrong assumption — surface the contradiction and confirm.

## Anti-patterns

- **Don't skip asking.** "I'll just start building" produces designs that miss the brief.
- **Don't ask everything.** A 30-question form is hostile. Cap around 10–15 for most work.
- **Don't ask one at a time across multiple turns.** Bundle into one form.
- **Don't ask about details you can derive.** If the user attached a brand guide with their primary color, don't ask what their primary color is.
