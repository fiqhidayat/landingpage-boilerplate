# AGENTS.md

Landing page boilerplate: Astro + Tailwind CSS, scaffolded via an AI skill instead of templates. Any agent that can read files, ask the user questions, and write files can run this — Claude Code, ChatGPT, LangChain, custom agents.

## Tech stack

- Astro 7.x (static site, no client JS framework)
- Tailwind CSS 4.x — CSS-based config, no `tailwind.config.js`. Theme tokens live in `src/styles/globals.css` under `@theme`.

## Dev commands

```bash
npm install
npm run dev       # localhost:4321, hot reload
npm run build     # → dist/
npm run preview   # serve the production build locally
```

Deploy: `wrangler pages deploy dist/` (Cloudflare Pages) or `docker compose up -d --build` (self-hosted, nginx on :8080). Full steps in `DEPLOYMENT.md`.

## Project structure

```
src/
  components/    Hero, Features, CTA, Footer (.astro)
  layouts/       Layout.astro
  pages/         index.astro (+ privacy.astro, terms.astro if generated)
  styles/        globals.css — brand color tokens (@theme)
public/assets/uploads/   user-supplied images/logo, referenced as /assets/uploads/<file>
```

## Skill: generate-landing-page

Interviews the user about a physical-product landing page and generates planning docs plus initial project config. No templates — every doc is written from scratch to current SaaS/e-commerce standards.

**Invoke:**
- Claude Code: `/generate-landing-page` (alias `/gen-lp`), or tell Claude to execute `.claude/skills/generate-landing-page/SKILL.md`
- Other agents: execute `.agents/skills/generate-landing-page/SKILL.md`

Both skill files are identical in content; only the path differs, so any agent that can read markdown can run the same workflow.

**What it does:**
1. Collects 15 fields — product name, category, description; 4 brand colors (hex); up to 2 design-reference URLs; target audience; 3 value props; whether to generate Privacy/Terms pages. Recommends a color scheme per category if the user doesn't have one.
2. Validates hex colors (`^#[0-9A-Fa-f]{6}$`) and URLs; re-asks on failure.
3. Generates `PRD.md`, `spec.md`, `tasks.md` (5-phase dev checklist), `progress.md`.
4. Writes brand colors into `src/styles/globals.css`, creates `src/pages/privacy.astro` / `terms.astro` if requested, creates `public/assets/uploads/`.

Claude Code additionally has `anti-ai-writing` and `hook-and-headline-writing` skills installed — the generate-landing-page skill calls them while drafting copy so PRD/marketing text doesn't read as AI-generated boilerplate.

## After generation

Work through `tasks.md`'s 5 phases (Design & Planning → Component Development → Page Assembly → Content & Copy → Polish & Deploy), tracking status in `progress.md`.
