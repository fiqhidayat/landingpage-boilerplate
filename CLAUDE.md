# Claude Configuration

Landing page boilerplate with AI-native skill definition.

## Project Overview

**Landing Page Boilerplate** — Astro + Tailwind CSS generator.

**Tech Stack:**
- Astro 4.x
- Tailwind CSS 3.x (v4 CSS-based config)

**Automation:** Skill-based, works with any AI agent.

---

## Generate Landing Page

### Command (Easiest)

```
/generate-landing-page
```

Alias: `/gen-lp`

### Instruction (Manual)

Tell Claude:

```
Execute the skill in .claude/skills/generate-landing-page/SKILL.md
```

### What It Does

1. **Gathers 14 fields:**
   - Product name, description
   - 4 brand colors (hex)
   - Design references (URLs)
   - Target audience
   - 3 value propositions
   - Privacy/Terms pages needed?

2. **Validates input**
   - Hex color format: `#RRGGBB`
   - URL basics
   - Re-asks if invalid

3. **Renders documentation:**
   - `PRD.md` — Product requirements
   - `spec.md` — Technical spec
   - `tasks.md` — Dev checklist (5 phases)
   - `progress.md` — Status tracker

4. **Updates project:**
   - `src/styles/globals.css` ← Brand colors
   - `src/pages/privacy.astro` (if requested)
   - `src/pages/terms.astro` (if requested)
   - `public/assets/uploads/` ← Ready for assets

5. **Optionally applies skills:**
   - `/anti-ai-writing` → Authentic messaging
   - `/copywriting` → Persuasive copy
   - `/frontend-design` → Design guidance

### Result

✅ Full project setup with:
- Generated documentation (4 files)
- Configured theme colors
- Ready for 5-phase development

---

## Skill Definition

**Location:** `.claude/skills/generate-landing-page/SKILL.md`

Contains:
- Input schema (14 fields)
- Step-by-step instructions for each document
- Industry standards for each doc type
- Quality criteria
- Legal page requirements
- Error handling
- Output schema

**All documents generated from scratch** following current SaaS industry standards.

**Portable:** Works with Claude, OpenAI, Anthropic, LangChain, custom agents.

---

## Important Notes

- User assets go in `/public/assets/uploads/`
- Theme config in `src/styles/globals.css` (@theme CSS directive)
- Components in `src/components/`
- Generated docs tracked in git
- Works with any LLM agent

---

## Development

```bash
npm install
npm run dev       # Start dev server
npm run build     # Production build
npm run preview   # Preview production
```

---

## After Generation

Development in 5 phases (see `tasks.md`):

1. **Design & Planning** (1-2h)
2. **Component Development** (4-8h)
3. **Page Assembly** (2-4h)
4. **Content & Copy** (2-3h)
5. **Polish & Deploy** (2-4h)

Track in `progress.md`
