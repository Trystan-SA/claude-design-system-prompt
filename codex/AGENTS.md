# Agent instructions

Load `system-prompt.md` as your operating instructions for any design task in this directory. It defines your role (designer, not code generator), workflow, and the skill library in `skills/`.

When a user request matches a skill description in `system-prompt.md` chapter 20, **read the corresponding file** from `skills/` and follow its phased procedure. Skills are reference documents — there is no skill-invocation tool in Codex; load them with a file read.

Verification is in-loop: render HTML output yourself (headless browser, Playwright, or `chrome-devtools`) and report findings as a short list. There is no verifier subagent.