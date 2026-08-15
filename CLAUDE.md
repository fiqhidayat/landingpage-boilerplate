# CLAUDE.md

Shared project context (tech stack, dev commands, skill workflow): see `AGENTS.md` — this file only covers Claude-specific behavior.

## Slash command

`/generate-landing-page` (alias `/gen-lp`) runs the skill at `.claude/skills/generate-landing-page/SKILL.md`.

## Skills installed for this project

- `generate-landing-page` — the main scaffolding skill (see AGENTS.md for what it does)
- `anti-ai-writing` — applied automatically while drafting PRD/marketing copy, to keep it from reading as AI-generated
- `hook-and-headline-writing` — applied for value-prop and headline copy
- `frontend-design` — invoke manually (`/frontend-design` or ask) when making visual/layout decisions during Component Development or Page Assembly

## Notes

- Generated docs (`PRD.md`, `spec.md`, `tasks.md`, `progress.md`) are tracked in git — commit them once generated.
- `.claude/skills/` and `.agents/skills/` hold identical skill content; edit both if changing the workflow, since Claude reads the former and other agents read the latter.
