# Agents & Automation

Universal landing page generation via skill definition.

**Any AI agent** (Claude, OpenAI, Anthropic, LangChain, custom) can execute this skill.

---

## Quick Start

**Claude users:**
```
Execute the skill in .claude/skills/generate-landing-page/SKILL.md
```

**Other agents (OpenAI, Anthropic, LangChain, etc):**
```
Execute the skill in .agents/skills/generate-landing-page/SKILL.md
```

**Workflow:**
1. Ask 14 required fields (product, colors, audience, value props, etc)
2. Validate input (hex colors, URLs)
3. Apply writing skills (anti-ai-writing, hook-and-headline-writing)
4. Generate PRD.md (industry standards)
5. Generate spec.md (technical requirements)
6. Generate tasks.md (5-phase development)
7. Generate progress.md (status tracker)
8. Create legal pages (if requested)
9. Update src/styles/globals.css
10. Create public/assets/uploads/ folder
11. Ready for development

---

## Skill Definition

**Locations:**
- Claude: `.claude/skills/generate-landing-page/SKILL.md`
- Others: `.agents/skills/generate-landing-page/SKILL.md`

**Contains:**
- Input schema (14 fields)
- Processing steps (4 phases)
- Output schema
- Error handling
- Example run

**Read this file → Execute → Output generated docs**

---

## How It Works

### Phase 1: Gather Requirements

14 fields:
```
product_name (string)
product_description (string)
color_primary (hex)
color_secondary (hex)
color_accent (hex)
color_neutral (hex)
design_reference_1 (url)
design_reference_2 (url, optional)
target_audience (string)
value_prop_1 (string)
value_prop_2 (string)
value_prop_3 (string)
include_privacy (bool)
include_terms (bool)
```

### Phase 2: Validate Input

- Hex colors: Match `^#[0-9A-Fa-f]{6}$`
- URLs: Basic validation
- If invalid: Ask user to correct

### Phase 3: Render Documentation

Templates in `.claude/templates/`:
- `PRD.md.template` → `PRD.md`
- `spec.md.template` → `spec.md`
- `tasks.md.template` → `tasks.md`
- `progress.md.template` → `progress.md`

Syntax:
- `{{variable}}` → Substitution
- `{{#if condition}}...{{/if}}` → Conditional

### Phase 4: Update Project

1. Update `src/styles/globals.css` with brand colors
2. Create `src/pages/privacy.astro` (if requested)
3. Create `src/pages/terms.astro` (if requested)
4. Create `public/assets/uploads/` folder

---

## Compatibility

| Agent | Path | Notes |
|-------|------|-------|
| Claude Code CLI | `.claude/skills/` | Can call skills directly |
| Claude API | `.claude/skills/` | Read skill file, execute |
| OpenAI GPT-4/o | `.agents/skills/` | Read skill file, execute |
| Anthropic API | `.agents/skills/` | Read skill file, execute |
| LangChain | `.agents/skills/` | Via custom executor |
| Custom agents | `.agents/skills/` | Any agent that can read/write files |

**Requirements:**
- Read files from .claude/ or .agents/ folders
- Accept user input (14 fields)
- Validate input (hex colors, URLs)
- Write output files
- Update existing files

**No scripts, no manual steps.** Pure AI-driven.

---

## Execution

**Claude users:**
```
Tell Claude: Execute skill in .claude/skills/generate-landing-page/SKILL.md
```

**Other agents:**
```
Tell agent: Execute skill in .agents/skills/generate-landing-page/SKILL.md
```

**Both paths:**
1. Read skill file
2. Collect 14 fields
3. Validate input
4. Apply writing skills (anti-ai-writing, hook-and-headline-writing)
5. Generate documentation
6. Update project files
7. Ready for development

Self-contained, portable, universal.

---

## Skill File Structure

```
.claude/skills/generate-landing-page/SKILL.md

├── Description
├── Input Schema (JSON)
├── Processing Steps (4 phases)
├── Output Schema (JSON)
├── Error Handling
├── Skills to Apply (Claude only)
└── Example Run
```

Everything needed to execute. Standalone.

---

## Document Generation

No templates. AI generates docs from scratch following industry standards.

**PRD.md** (Industry-standard Product Requirements)
- Executive summary
- Product overview & branding
- Value propositions
- Target audience & pain points
- Features & functionality
- Success metrics
- Design references analysis

**spec.md** (Industry-standard Technical Spec)
- Technical stack overview
- Architecture design
- Project structure
- Component specifications
- Design system guidelines
- Performance targets (Lighthouse 90+)
- Accessibility (WCAG 2.1 AA)
- SEO implementation
- Deployment requirements

**tasks.md** (Agile-style Development Checklist)
- 5 sequential phases with time estimates
- Actionable checkboxes per phase
- QA criteria for each phase
- Component breakdown
- Testing requirements
- Deployment checklist
- Post-launch tasks

**progress.md** (Project Management Tracker)
- Real-time phase progress
- Metrics dashboard
- Blocker/issue tracking
- Team notes
- Launch readiness checklist
- Status indicators

**Legal pages** (if requested)
- Privacy Policy (GDPR/CCPA compliant)
- Terms of Service (standard legal structure)

---

## What Gets Generated

**Documentation files:**
- `PRD.md` (Product Requirements Document)
- `spec.md` (Technical Specification)
- `tasks.md` (5-phase development checklist)
- `progress.md` (Project status tracker)

**Pages (if requested):**
- `src/pages/privacy.astro` (Privacy Policy)
- `src/pages/terms.astro` (Terms of Service)

**Project updates:**
- `src/styles/globals.css` (brand colors injected)
- `public/assets/uploads/` (asset folder created)

**Result:** Ready-to-develop landing page project with all docs.

---

## Error Handling

Skill file includes error cases:
- Invalid hex colors
- Invalid URLs
- Missing templates
- File write failures

AI agent should handle per error handling section in skill file.

---

## Why This Approach

✅ **Clean:** No scripts, no boilerplate
✅ **Universal:** Works with any AI agent
✅ **Portable:** Skill is just documentation
✅ **AI-native:** Designed for LLM agents to read & execute
✅ **Offline:** No external dependencies
✅ **Deterministic:** Same input = same output
✅ **Versionable:** Committed to git

