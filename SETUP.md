# Setup Guide

Complete walkthrough for using the Landing Page Boilerplate with Claude Code.

## Prerequisites

- Node.js 16+ and npm
- Claude Code CLI installed
- Git

## Installation

### 1. Fork the Repository

On GitHub:
```
https://github.com/youruser/landing-page-boilerplate
```

### 2. Clone Locally

```bash
git clone https://github.com/youruser/landing-page-boilerplate.git
cd landing-page-boilerplate
```

### 3. Install Dependencies

```bash
npm install
```

## First Run: Generate Landing Page

### Any AI Agent

Tell your AI agent:

```
Execute the skill in .claude/skills/generate-landing-page/SKILL.md
```

This applies to:
- Claude Code (CLI/Desktop/Web)
- Claude API
- OpenAI GPT-4/o
- Anthropic API
- LangChain agents
- Custom agents

---

### AI will then:

### Skill Inputs (14 Fields)

AI will ask for:

1. **Product name** — Full name (e.g., "SyncFlow Pro")
2. **Product description** — 1-2 sentences
3. **Primary color** — Hex code (e.g., `#3b82f6`)
4. **Secondary color** — Hex code (e.g., `#1e40af`)
5. **Accent color** — Hex code (e.g., `#f59e0b`)
6. **Neutral color** — Hex code (e.g., `#f3f4f6`)
7. **Design reference 1** — Website URL (e.g., `https://stripe.com`)
8. **Design reference 2** — Website URL (optional)
9. **Target audience** — Who is this for? (e.g., "SaaS founders")
10. **Value prop 1** — Key benefit
11. **Value prop 2** — Key benefit
12. **Value prop 3** — Key benefit
13. **Include Privacy Policy?** — yes/no
14. **Include Terms of Service?** — yes/no

### Validation

AI validates:
- Hex colors: Format `#RRGGBB`
- URLs: Basic validity check
- Asks to correct if invalid

### Generated Documentation

4 files created by AI (industry-standard format):

**PRD.md** — Product Requirements Document
- Executive summary with product vision
- Brand identity (colors, design philosophy)
- Detailed value propositions
- Target audience & pain points
- Features & functionality
- Success metrics & KPIs

**spec.md** — Technical Specification
- Astro + Tailwind architecture
- Component specifications with accessibility
- Design system guidelines
- Performance targets (Lighthouse 90+)
- WCAG 2.1 AA compliance requirements
- SEO implementation plan
- Deployment strategy

**tasks.md** — Development Checklist
- 5 sequential phases (1-2, 4-8, 2-4, 2-3, 2-4 hours)
- Actionable checkboxes per phase
- Component breakdown with responsive requirements
- Testing criteria (mobile, tablet, desktop)
- Accessibility & performance audits
- Post-launch deployment checklist

**progress.md** — Status Tracker
- Real-time phase progress tracking
- Metrics dashboard (Lighthouse, Core Web Vitals, etc)
- Blocker/issue documentation
- Team notes & decision log
- Launch readiness checklist
- Phase completion percentages

### Project Setup

AI automatically:

1. **Updates `src/styles/globals.css`** — Injects brand colors into @theme block
2. **Creates legal pages** (if requested)
   - `src/pages/privacy.astro`
   - `src/pages/terms.astro`
3. **Creates asset folder** — `public/assets/uploads/` ready
4. **Project ready** — For immediate development

## Next: Development

After execution, your project is ready. Start the dev server:

```bash
npm run dev
```

Open http://localhost:3000 in your browser.

### Development Phases

Follow the 5-phase workflow:

#### Phase 1: Design & Planning
- Review PRD and design references
- Finalize color palette
- Plan component hierarchy
- Define typography

**Duration:** 1-2 hours

#### Phase 2: Component Development
- Build reusable components
- Style with Tailwind
- Test responsive design
- Implement interactivity

**Duration:** 4-8 hours

#### Phase 3: Page Assembly
- Integrate components
- Build main landing page
- Responsive optimization
- Layout refinements

**Duration:** 2-4 hours

#### Phase 4: Content & Copy
- Implement copywriting
- Add SEO meta tags
- Legal pages (if needed)
- Final copy review

**Duration:** 2-3 hours

#### Phase 5: Polish & Deploy
- Performance optimization
- Accessibility audit
- Cross-browser testing
- Build & deploy

**Duration:** 2-4 hours

**Total Estimated Time:** 11-21 hours

## Adding Assets

Place your files in `/public/assets/uploads/`:

```bash
# Example
public/assets/uploads/
├── logo.svg
├── hero-bg.png
├── feature-1.png
├── feature-2.png
└── product-screenshot.png
```

Reference in Astro components:

```astro
<img src="/assets/uploads/hero-bg.png" alt="Hero Background" />
```

## After Generation: Development

Follow the 5-phase workflow in `tasks.md`:

1. **Design & Planning** (1-2 hours)
   - Review PRD and design references
   - Finalize color palette
   - Plan component hierarchy

2. **Component Development** (4-8 hours)
   - Build reusable components
   - Style with Tailwind
   - Test responsive design

3. **Page Assembly** (2-4 hours)
   - Integrate components
   - Build main landing page
   - Responsive optimization

4. **Content & Copy** (2-3 hours)
   - Implement copywriting
   - Add SEO meta tags
   - Add legal pages

5. **Polish & Deploy** (2-4 hours)
   - Performance optimization
   - Accessibility audit
   - Production build & deploy

---

## Customization

### Brand Colors

Edit `src/styles/globals.css` @theme block:

```css
@theme {
  --color-primary: #NewColor;
  --color-secondary: #NewColor;
  --color-accent: #NewColor;
  --color-neutral: #NewColor;
}
```

### Add Custom Fonts

In `src/layouts/Layout.astro` `<head>`:

```html
<link
  href="https://fonts.googleapis.com/css2?family=YourFont:wght@400;700&display=swap"
  rel="stylesheet"
/>
```

Update `src/styles/globals.css` @theme block:

```css
@theme {
  --font-sans: 'Your Font', system-ui, sans-serif;
}
```

### Modify Components

All components are in `src/components/`. Edit them directly:

```astro
// src/components/Hero.astro
---
// Your content here
---

<section class="min-h-screen ...">
  <!-- Your HTML -->
</section>
```

### Add New Pages

Create files in `src/pages/`:

```bash
# This automatically becomes /about route
touch src/pages/about.astro
```

```astro
---
import Layout from '../layouts/Layout.astro';
---

<Layout title="About">
  <!-- Your content -->
</Layout>
```

## Building for Production

```bash
npm run build
```

Output in `dist/` folder. Ready to deploy to:
- Vercel
- Netlify
- AWS S3
- GitHub Pages
- Any static host

## Troubleshooting

### Skill execution not working?

Ensure your AI agent can:
- Read `.claude/skills/generate-landing-page/SKILL.md`
- Accept user input (14 fields)
- Write files to project root
- Update existing files

### Build errors?

```bash
# Clean and rebuild
rm -rf node_modules dist .astro
npm install
npm run build
```

### Assets not loading?

1. Check file exists: `public/assets/uploads/filename`
2. Use correct path: `/assets/uploads/filename` (not `./assets/uploads/`)
3. Check browser console for 404 errors

### Styling issues?

1. Ensure Tailwind CSS is building (check `npm run dev` output)
2. Verify file is in `src/` directory (Tailwind scans these)
3. Restart dev server: `Ctrl+C` then `npm run dev`

## Project Structure

After skill execution, you'll have:

```
landing-page-boilerplate/
├── .claude/
│   ├── settings.json              ← Claude Code config
│   └── skills/
│       └── generate-landing-page/
│           └── SKILL.md    ← AI skill definition
├── src/
│   ├── components/
│   │   ├── Hero.astro
│   │   ├── Features.astro
│   │   ├── CTA.astro
│   │   └── Footer.astro
│   ├── layouts/
│   │   └── Layout.astro           ← Base layout with theme
│   ├── pages/
│   │   ├── index.astro            ← Home page
│   │   ├── privacy.astro          ← Generated if needed
│   │   └── terms.astro            ← Generated if needed
│   └── styles/
│       └── globals.css            ← Tailwind @theme config
├── public/
│   ├── assets/
│   │   └── uploads/               ← Your images go here
│   └── favicon.svg
├── .gitignore
├── astro.config.mjs
├── package.json
├── README.md
├── SETUP.md                       ← This file
├── CLAUDE.md                      ← Claude Code docs
├── AGENTS.md                      ← Multi-agent flow docs
├── PRD.md                         ← Generated by skill
├── spec.md                        ← Generated by skill
├── tasks.md                       ← Generated by skill
└── progress.md                    ← Generated by skill
```

## Next Steps

1. ✅ Installation complete
2. Execute skill to generate documentation
3. Review generated `PRD.md`, `spec.md`, `tasks.md`
4. Follow 5-phase development workflow
5. Deploy with `npm run build`

## Questions?

- Read `CLAUDE.md` for Claude Code integration details
- Read `AGENTS.md` for multi-agent workflow details
- Check `README.md` for quick reference
- Review generated `spec.md` for technical details

---

**Ready? Let's build! 🚀**
