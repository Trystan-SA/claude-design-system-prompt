# Claude Design System Prompt

Reverse-engineered system prompt of Claude Design from Anthropic.

A system prompt and skill library that turns an LLM into an opinionated, accessibility-aware, AI-slop-resistant design collaborator.

Open source, MIT licensed. Drop the prompt into any LLM that supports system prompts (Claude, GPT, Gemini, local models) and pair with the procedural skills as needed.

## What this is

Most "design assistant" prompts produce generic SaaS-template output — aggressive gradients, emoji decoration, rounded-corner-with-left-border cards, Inter-everywhere typography. This prompt explicitly rejects those patterns and replaces them with a complete design philosophy covering:

- Content discipline (no filler — every element earns its place)
- Aesthetic discipline (avoid AI tropes, commit to a palette and tone)
- Visual hierarchy and rhythm (size, color, weight, position, density, spacing scales)
- Accessibility (WCAG, semantic HTML, keyboard navigation, focus rings, motion preferences)
- Interaction and feedback (hover, active, disabled, focus, loading, validation states)
- System thinking (components and tokens over one-off pages)
- Respecting the medium (real CSS Grid, `oklch()`, `text-wrap: pretty`, real interactive prototypes)
- Quality over quantity (depth over breadth, polish every detail)

Plus 14 procedural skills the agent can invoke for production, extraction, and review work.

## What's included

```
claude-design-system-prompt/
├── claude/                              Claude Code / Claude.ai variant
│   ├── system-prompt.md                 Main system prompt — 20 chapters
│   └── skills/                          14 invokable skills
│       ├── discovery-questions.md       Kickoff question protocol
│       ├── frontend-aesthetic-direction.md  Commit to a look when no brand exists
│       ├── wireframe.md                 Low-fi exploration, 3+ variations
│       ├── make-a-deck.md               Slide presentations in HTML
│       ├── make-a-prototype.md          Interactive clickable prototype
│       ├── make-tweakable.md            Floating tweak panel
│       ├── generate-variations.md       3+ hi-fi variations across axes
│       ├── design-system-extract.md     Pull tokens from sources
│       ├── component-extract.md         Inventory reusable components
│       ├── accessibility-audit.md       WCAG, semantic, keyboard, motion
│       ├── ai-slop-check.md             Gradient / emoji / font trope detection
│       ├── hierarchy-rhythm-review.md   Size / weight / color + spacing scale
│       ├── interaction-states-pass.md   Hover / active / disabled / focus / loading
│       └── polish-pass.md               Umbrella final-gate review
├── codex/                               OpenAI Codex variant (single-loop, no subagents)
│   ├── AGENTS.md                        Codex auto-discovered entry point
│   ├── system-prompt.md                 Same prompt, adapted for Codex
│   └── skills/                          Same skills, sequential reviews instead of parallel agents
├── README.md                            This file
└── LICENSE                              MIT
```

## How to use it

### Use the system prompt directly

Paste the contents of `system-prompt.md` as the system prompt for any LLM that supports them. The agent will follow the design philosophy and reference the skills by name when tasks match.

### Use the skills as procedures

Each skill in `skills/` is a self-contained, phased procedure. The skill name is the trigger — when the user's request matches a skill description, the agent loads that skill and follows it.

Skills group into three categories:

**Production** — build something
`discovery-questions` · `frontend-aesthetic-direction` · `wireframe` · `make-a-deck` · `make-a-prototype` · `make-tweakable` · `generate-variations`

**System** — extract structure
`design-system-extract` · `component-extract`

**Review** — audit and fix
`accessibility-audit` · `ai-slop-check` · `hierarchy-rhythm-review` · `interaction-states-pass` · `polish-pass`

Skills can be chained. A typical greenfield flow:

```
discovery-questions → frontend-aesthetic-direction → wireframe → make-a-prototype → polish-pass
```

A brand-aware flow:

```
design-system-extract → generate-variations → make-tweakable → polish-pass
```

### Adapt for your platform

The prompt assumes an HTML-output design environment (similar to Claude.ai's design tool). If your target environment is different — a Figma plugin, a code-only assistant, a chat-only design coach — you'll need to adjust the workflow chapters and tool references. The principles (chapters 5–16) translate to any medium.

## Design principles, in short

The 20 chapters in `system-prompt.md` cover:

| #   | Chapter                                   |
| --- | ----------------------------------------- |
| 1   | Identity and role                         |
| 2   | Workflow                                  |
| 3   | Asking questions first                    |
| 4   | Rooting designs in existing context       |
| 5   | Content principles — no filler            |
| 6   | Aesthetic principles — purposeful visuals |
| 7   | Visual hierarchy and rhythm               |
| 8   | Typography system                         |
| 9   | Color system                              |
| 10  | Accessibility and inclusivity             |
| 11  | Interaction and feedback                  |
| 12  | Simplicity and one clear CTA              |
| 13  | System thinking                           |
| 14  | Respecting the medium                     |
| 15  | Understanding users                       |
| 16  | Quality over quantity                     |
| 17  | Output principles                         |
| 18  | Collaboration and delivery                |
| 19  | IP and content boundaries                 |
| 20  | Available skills                          |

## Contributing

Issues and PRs welcome. Particularly useful contributions:

- Additional review skills (e.g., copy review, motion review, dark-mode parity check)
- Adapted prompts for other environments (Figma, code-only, terminal-only)
- Real-world failure cases the prompt should defend against
- Translations of the prompt into other languages

Please keep the same operational tone and avoid bloating the prompt — every chapter should earn its place, the same standard the prompt holds the agent to.

## License

MIT — see `LICENSE`.

You can use, modify, and distribute this prompt and skill library for any purpose, including commercial use. No attribution required, but appreciated.
