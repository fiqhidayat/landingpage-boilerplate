# Agents Configuration

Skills and configuration for non-Claude AI agents (OpenAI, Anthropic API, LangChain, etc).

## Skills

**Location:** `.agents/skills/`

### generate-landing-page/SKILL.md
**Main skill:** Auto-generate landing page documentation from product requirements.

**Entry point:** Read `.agents/skills/generate-landing-page/SKILL.md`

**Flow:**
1. Ask user for 14 fields (product, colors, audience, value props, etc)
2. Validate input (hex colors, URLs)
3. Apply writing skills (Step 1.5)
4. Generate PRD.md, spec.md, tasks.md, progress.md
5. Update src/styles/globals.css
6. Create legal pages if requested
7. Ready for development

### anti-ai-writing
**Purpose:** Transform AI-assisted drafts into authentic, human-sounding content.

**Location:** `.agents/skills/anti-ai-writing/SKILL.md`

**Applied in Step 1.5:**
- Product description
- Value propositions (3x)

**Framework:** SUCKS (Specific, Unique, Clear, Kept Simple, Sticky)

**How to use:**
```
Read .agents/skills/anti-ai-writing/SKILL.md
Apply SUCKS framework to:
- product_description
- value_prop_1, value_prop_2, value_prop_3
```

### hook-and-headline-writing
**Purpose:** Create attention-grabbing headlines and hooks.

**Location:** `.agents/skills/hook-and-headline-writing/SKILL.md`

**Applied in Step 1.5:**
- Headlines
- Taglines
- CTA copy

**Framework:** 4 U's Test (Useful, Unique, Urgent, Ultra-specific)

**How to use:**
```
Read .agents/skills/hook-and-headline-writing/SKILL.md
Apply 4 U's test to:
- PRD.md headlines
- Taglines
- All CTA copy
Generate 5+ options per headline, pick best
```

## How to Execute

**For any AI agent (OpenAI, Anthropic, LangChain, etc):**

1. Read `.agents/skills/generate-landing-page/SKILL.md`
2. Follow the workflow step-by-step
3. Use skill files as reference for writing frameworks
4. Generate output files

**Example instruction:**

```
Execute the skill in .agents/skills/generate-landing-page/SKILL.md:

1. Ask me 14 fields (product, colors, audience, etc)
2. Validate input
3. Apply anti-ai-writing skill (read .agents/skills/anti-ai-writing/SKILL.md)
4. Apply hook-and-headline-writing skill (read .agents/skills/hook-and-headline-writing/SKILL.md)
5. Generate PRD.md, spec.md, tasks.md, progress.md
6. Update src/styles/globals.css with colors
7. Create legal pages if requested
8. Create public/assets/uploads/ folder
9. Done!
```

## For Claude Users

Use `.claude/skills/` instead:

```
Execute the skill in .claude/skills/generate-landing-page/SKILL.md
```

Claude can call skills directly:
- `/anti-ai-writing`
- `/hook-and-headline-writing`

## Compatibility

✅ OpenAI GPT-4/o
✅ Anthropic API
✅ LangChain agents
✅ Custom LLM agents
✅ Any system that can read files and execute instructions
