---
name: generate-landing-page
description: Generate landing page documentation (PRD, spec, tasks, progress) for physical product sellers - Food & Beverage, Fashion, Electronics, Home & Garden, Beauty, Toys, Sports, B2B, etc. Use when a user wants to scaffold a new product landing page, needs brand color recommendations, or asks to run /generate-landing-page or /gen-lp. Works with any LLM agent (Claude, OpenAI, LangChain, etc).
---

# Generate Landing Page (Physical Products)

---

## Input Collection

Gather 15 fields from user:

```json
{
  "product_name": "string (required)",
  "product_category": "enum (required)",
  "product_description": "string, 1-2 sentences (required)",
  "color_primary": "hex #RRGGBB (required or recommended)",
  "color_secondary": "hex #RRGGBB (required or recommended)",
  "color_accent": "hex #RRGGBB (required or recommended)",
  "color_neutral": "hex #RRGGBB (required or recommended)",
  "design_reference_1": "url (required)",
  "design_reference_2": "url (optional)",
  "target_audience": "string (required)",
  "value_prop_1": "string (required)",
  "value_prop_2": "string (required)",
  "value_prop_3": "string (required)",
  "include_privacy": "boolean (yes/no)",
  "include_terms": "boolean (yes/no)"
}
```

**Product Categories:**
1. Food & Beverage
2. Fashion & Apparel
3. Electronics
4. Home & Garden
5. Beauty & Personal Care
6. Toys & Games
7. Sports & Outdoors
8. Company/B2B Services
9. SaaS (minority option)
10. Other (custom)

---

## Step 1: Product Name & Category

**Ask user:**
```
1. Product name: [e.g., "Premium Coffee Beans"]
2. Product category: [Choose from list above]
```

---

## Step 1.5: Recommend Color Scheme

**Based on category, recommend colors:**

**Food & Beverage:**
- Primary: Warm (Orange #FF8C00, Red #E63946, Brown #8B4513)
- Secondary: Gold #D4AF37, Cream #FFF8DC
- Why: Appetizing, trustworthy, premium feel

**Fashion & Apparel:**
- Primary: Trendy (Black #1F1F1F, Navy #001F3F, Rose Gold #B76E79)
- Secondary: White #FFFFFF, accent varies (Emerald #50C878, Gold #FFD700)
- Why: Luxury, modern, matches brand positioning

**Electronics:**
- Primary: Modern (Blue #0066CC, Gray #4A4A4A, Silver #C0C0C0)
- Secondary: Black #000000, accent (Cyan #00D4FF)
- Why: Tech-forward, professional, trustworthy

**Home & Garden:**
- Primary: Natural (Green #2D5016, Brown #8B7355, Terracotta #CC6655)
- Secondary: White #FFFFFF, Beige #F5F5DC
- Why: Organic, calming, natural

**Beauty & Personal Care:**
- Primary: Premium (Rose Gold #B76E79, Blush #FFB6C1, White #FFFFFF)
- Secondary: Gold #FFD700, Lavender #E6B0E0
- Why: Luxury, sophisticated, aspirational

**Toys & Games:**
- Primary: Bright (Red #FF0000, Blue #0000FF, Yellow #FFFF00)
- Secondary: Green #00FF00, Pink #FF69B4, Orange #FFA500
- Why: Playful, energetic, engaging

**Sports & Outdoors:**
- Primary: Dynamic (Blue #1E3A8A, Green #22C55E, Red #DC2626)
- Secondary: Black #000000, Gray #6B7280
- Why: Active, energetic, professional

**B2B Services:**
- Primary: Professional (Blue #003366, Gray #4A5568, Navy #001F3F)
- Secondary: White #FFFFFF, Light Gray #E8EAED
- Why: Trustworthy, corporate, serious

**Offer to user:**
```
Based on your {{category}} category, we recommend:

Primary: {{recommended_hex}} ({{color_name}})
  Reasoning: {{reason}}

Secondary: {{recommended_hex}} ({{color_name}})
Accent: {{recommended_hex}} ({{color_name}})
Neutral: {{recommended_hex}} ({{color_name}})

Accept these recommendations? (yes/no)
If no: Provide your custom hex colors
```

**If user accepts:** Use recommendations
**If user declines:** Ask for custom colors

---

## Step 2: Validate Input

### Hex Colors
- Format: `^#[0-9A-Fa-f]{6}$`
- If invalid → Ask user to provide correct hex
- Example valid: `#3b82f6`

### URLs
- Check valid URL format
- If invalid → Ask user to correct

---

## Step 3: Apply Writing Skills (Claude Only)

**For Claude users:** Elevate copy quality with installed writing skills.

### Apply `/anti-ai-writing` Skill

**Location:** `.claude/skills/anti-ai-writing/`

**Apply to:** `product_description`, `value_prop_1`, `value_prop_2`, `value_prop_3`

**Purpose:** Transform AI-assisted drafts into authentic, human-sounding content. Eliminates AI patterns while maintaining clarity.

**How to use:**
```
Execute anti-ai-writing skill on:
- Product description
- All 3 value propositions

Follow SUCKS framework from skill
```

**Result:** Copy that reads authentic, not AI-generated.

---

### Apply `/hook-and-headline-writing` Skill

**Location:** `.claude/skills/hook-and-headline-writing/`

**Apply to:** Headlines, taglines, CTA copy in PRD.md and spec.md

**Purpose:** Create attention-grabbing headlines using 15 proven formulas and 4 U's test.

**How to use:**
```
Execute hook-and-headline-writing skill on:
- PRD.md executive summary headline
- Product tagline
- All CTA copy
- Spec.md section headers

Generate 5+ options per headline, select best via 4 U's test
```

**Result:** Headlines that stop the scroll and compel action.

---

## Step 4: Generate PRD.md (Product Requirements Document)

**Standards:** Follow physical product (e-commerce) industry best practices.

**Structure:**
```
1. Executive Summary
   - 1-2 paragraphs about product vision
   - Why this product exists
   - Problem it solves for customers

2. Product Overview
   - Product name & tagline
   - One-sentence description
   - Category: {{product_category}}
   - Target market
   - Price positioning (if known)

3. Brand & Visual Identity
   - Primary brand color + hex (recommended: {{color_recommendation}})
   - Secondary brand color + hex
   - Accent color + hex
   - Neutral color + hex
   - Design philosophy for {{category}} (from references provided)

4. Value Propositions
   - 3+ compelling benefits (enhanced via /anti-ai-writing skill)
   - Include "why customers should buy" not just features
   - Show competitive advantages with concrete examples
   - Clear, specific, benefit-focused for {{target_audience}}

5. Target Audience
   - Detailed audience description
   - Shopping behaviors & preferences
   - Pain points/needs addressed
   - Buying triggers

6. Product Specifications
   - Physical dimensions/weight
   - Materials/composition
   - Variants/options available
   - Packaging details
   - Shelf life (if applicable)

7. Shipping & Fulfillment
   - Shipping methods
   - Estimated delivery times
   - Return policy
   - Warranty/guarantee

8. Success Metrics
   - How success is measured (sales, reviews, repeat customers)
   - Key performance indicators
   - Revenue goals
   - Customer satisfaction targets

9. Design References
   - List provided design references
   - What to learn from each for {{category}}
```

**Style:**
- Customer-focused, benefit-driven
- Clear value focus
- Concrete product details
- E-commerce industry terminology
- Category-specific guidance

---

## Step 5: Generate spec.md (Technical Specification)

**Standards:** Follow e-commerce/product landing page best practices.

**Structure:**
```
1. Technical Stack
   - Astro 4.x (static site generation)
   - Tailwind CSS v4 (CSS-based config)
   - {{category}}-optimized architecture

2. Architecture Overview
   - E-commerce focused design
   - Product showcase system
   - Shopping/contact flow
   - High-speed, conversion-optimized

3. Page Components
   - Hero: Product showcase
   - Product Details: Specs, pricing, variants
   - Image Gallery: High-quality product photos
   - Reviews/Social Proof: Customer testimonials
   - CTA/Contact: Purchase or inquiry
   - Footer: Shipping, returns, contact

4. Product Display System
   - Product image optimization (WebP, compression)
   - Variant selector (size, color, options)
   - Price display & discounts
   - Inventory status indicators
   - Customer reviews/ratings

5. Design System ({{color_primary}}, {{color_secondary}})
   - Color palette for {{category}}
   - Typography (readability for product details)
   - Spacing scale
   - Button states (add to cart, out of stock, etc)
   - Category-appropriate styling

6. E-commerce Features
   - Shopping cart integration point (e.g., Shopify, WooCommerce)
   - Payment gateway readiness
   - Inventory tracking capability
   - Order tracking information
   - Upsell/cross-sell opportunities

7. Performance & Conversion
   - Lighthouse score targets (90+)
   - Core Web Vitals targets
   - Image optimization (product photos < 200KB)
   - Fast load times (critical for conversion)
   - Mobile-first responsive design

8. Accessibility Standards
   - WCAG 2.1 AA compliance
   - Product images: Descriptive alt text
   - Color contrast: 4.5:1 minimum
   - Keyboard navigation for all interactive elements
   - Form accessibility (checkout, contact)

9. SEO for {{category}}
   - Meta tags: Product name, description, price
   - Structured data: Product schema.org markup
   - Image SEO: Alt text with keywords
   - Reviews schema (if applicable)
   - Mobile-friendly mobile verification
   - Fast load for search ranking

10. Integration Points
   - E-commerce platform (Shopify, WooCommerce, custom)
   - Payment processor (Stripe, PayPal, etc)
   - Email for orders & follow-up
   - Analytics (Google Analytics 4)
   - Social media sharing
```

**Style:**
- Customer-conversion focused
- Specific product requirements
- E-commerce integration points clear
- {{category}}-specific guidance
- Mobile-first (majority shop on phone)

---

## Step 6: Generate tasks.md (Development Checklist)

**Standards:** Follow agile/sprint methodology with clear phases.

**Structure:**
```
# Tasks: {{product_name}}

## Overview
- Product: {{product_name}}
- Timeline: Estimated {{X}} hours total
- Phases: 5 sequential phases

---

## Phase 1: Design & Planning (1-2 hours)
**Goal:** Finalize visual direction and component strategy

- [ ] Review PRD.md and design references
- [ ] Extract design patterns from references
- [ ] Define color palette application rules
- [ ] Create typography hierarchy
- [ ] Plan responsive breakpoints (mobile/tablet/desktop)
- [ ] Document component hierarchy
- [ ] Identify common patterns & reusable elements

**Deliverables:**
- Design decisions documented
- Component list finalized

---

## Phase 2: Component Development (4-8 hours)
**Goal:** Build reusable, accessible Tailwind components

- [ ] Create Hero component
  - [ ] Responsive layout
  - [ ] Background image/gradient support
  - [ ] CTA button
  - [ ] Mobile-optimized

- [ ] Create Features section component
  - [ ] Grid layout (1 col mobile, 2-3 col desktop)
  - [ ] Feature cards with icons
  - [ ] {{value_prop_1}}, {{value_prop_2}}, {{value_prop_3}}

- [ ] Create Product/Services showcase
  - [ ] Image carousel or grid
  - [ ] Product details
  - [ ] CTA per item

- [ ] Create Contact/Form component
  - [ ] Email validation
  - [ ] Required fields
  - [ ] Success/error states

- [ ] Create CTA section
  - [ ] Headline
  - [ ] Primary button
  - [ ] Secondary option

- [ ] Create Footer component
  - [ ] Company info
  - [ ] Links (legal pages)
  - [ ] Social links
  - [ ] Copyright

**Testing:**
- [ ] Mobile view (320px)
- [ ] Tablet view (768px)
- [ ] Desktop view (1920px)
- [ ] Accessibility (keyboard nav, color contrast)

---

## Phase 3: Page Assembly (2-4 hours)
**Goal:** Integrate components into cohesive landing page

- [ ] Build main landing page (src/pages/index.astro)
- [ ] Integrate all components in logical flow
- [ ] Verify responsive design across breakpoints
- [ ] Test component interactions
- [ ] Optimize spacing & alignment
- [ ] Review visual hierarchy

**Quality Checks:**
- [ ] Lighthouse audit (90+ score)
- [ ] Mobile-first responsive test
- [ ] Cross-browser testing

---

## Phase 4: Content & Copy (2-3 hours)
**Goal:** Implement compelling messaging and SEO

- [ ] Review copywriting guidelines
- [ ] Implement headlines from PRD
- [ ] Implement value propositions
- [ ] Write compelling descriptions
- [ ] Add meta tags (title, description)
- [ ] Add OG tags (social sharing)
- [ ] Implement schema.org structured data
{{#if include_privacy}}
- [ ] Create Privacy Policy page (src/pages/privacy.astro)
  - [ ] Legal compliance requirements
  - [ ] Data collection disclosure
  - [ ] Cookie policy
{{/if}}
{{#if include_terms}}
- [ ] Create Terms of Service page (src/pages/terms.astro)
  - [ ] User obligations
  - [ ] Liability limitations
  - [ ] Dispute resolution
{{/if}}

**Copywriting Focus:**
- [ ] Clear value communication
- [ ] Action-oriented CTAs
- [ ] Trust-building language
- [ ] Mobile-friendly reading length

---

## Phase 5: Polish & Deploy (2-4 hours)
**Goal:** Optimize, audit, and launch

**Performance:**
- [ ] Minimize images (WebP format)
- [ ] Remove unused CSS
- [ ] Optimize font loading
- [ ] Enable compression
- [ ] Test Core Web Vitals

**Accessibility Audit:**
- [ ] WCAG 2.1 AA compliance check
- [ ] Keyboard navigation test
- [ ] Screen reader test
- [ ] Color contrast verification
- [ ] Alt text on all images

**Security:**
- [ ] HTTPS enabled
- [ ] Security headers configured
- [ ] No hardcoded secrets

**Testing:**
- [ ] Chrome/Firefox/Safari/Edge
- [ ] Mobile devices (iPhone, Android)
- [ ] Tablet devices
- [ ] Network throttling test

**Production Build:**
- [ ] npm run build
- [ ] Test dist/ output
- [ ] npm run preview

**Deployment:**
- [ ] Choose hosting (Vercel, Netlify, AWS, etc)
- [ ] Configure domain
- [ ] Deploy to production
- [ ] Verify live site
- [ ] Set up analytics
- [ ] Monitor performance

**Post-Launch:**
- [ ] Share landing page
- [ ] Collect feedback
- [ ] Monitor metrics
- [ ] Plan iterations

---

## Time Estimates

- Phase 1: 1-2 hours
- Phase 2: 4-8 hours
- Phase 3: 2-4 hours
- Phase 4: 2-3 hours
- Phase 5: 2-4 hours

**Total: 11-21 hours** from start to production

---

## Asset Management

**Location:** `/public/assets/uploads/`

**Required:**
- Logo (SVG preferred, PNG fallback)
- Hero image (optimized for web)

**Optional:**
- Product screenshots
- Icons/graphics
- Social media images

---

## Development Workflow

1. Clone project
2. `npm install`
3. `npm run dev` (start dev server)
4. Follow phases in order
5. Commit progress to git
6. `npm run build` when ready
7. Deploy to hosting
```

**Style:**
- Actionable checkboxes
- Clear phase breakdown
- Time estimates
- Specific deliverables
- QA criteria included

---

## Step 7: Generate progress.md (Status Tracker)

**Standards:** Follow project management best practices.

**Structure:**
```
# Project Progress: {{product_name}}

**Generated:** {{date}}
**Status:** ⏳ Not Started
**Overall Completion:** 0%

---

## Project Overview

| Metric | Value |
|--------|-------|
| Product | {{product_name}} |
| Description | {{product_description}} |
| Target Audience | {{target_audience}} |
| Timeline | ~11-21 hours |
| Estimated Launch | [Add date] |

---

## Phase Progress

### Phase 1: Design & Planning
**Status:** ⏳ Not Started
**Completion:** 0%
**Timeline:** 1-2 hours

**Checklist:**
- [ ] Review design references
- [ ] Define design system
- [ ] Plan component hierarchy
- [ ] Document typography
- [ ] Finalize responsive strategy

**Notes:**
- [Add notes as you progress]

---

### Phase 2: Component Development
**Status:** ⏳ Not Started
**Completion:** 0%
**Timeline:** 4-8 hours

**Component Checklist:**
- [ ] Hero (0%)
- [ ] Features (0%)
- [ ] Showcase (0%)
- [ ] CTA (0%)
- [ ] Contact Form (0%)
- [ ] Footer (0%)

**Notes:**
- [Add notes as you progress]

---

### Phase 3: Page Assembly
**Status:** ⏳ Not Started
**Completion:** 0%
**Timeline:** 2-4 hours

**Checklist:**
- [ ] Integrate components
- [ ] Test responsiveness
- [ ] Verify visual hierarchy
- [ ] Performance audit
- [ ] Cross-browser test

**Notes:**
- [Add notes as you progress]

---

### Phase 4: Content & Copy
**Status:** ⏳ Not Started
**Completion:** 0%
**Timeline:** 2-3 hours

**Checklist:**
- [ ] Implement headlines
- [ ] Add meta tags
- [ ] Write descriptions
- [ ] Create legal pages (if needed)
- [ ] SEO optimization

**Notes:**
- [Add notes as you progress]

---

### Phase 5: Polish & Deploy
**Status:** ⏳ Not Started
**Completion:** 0%
**Timeline:** 2-4 hours

**Checklist:**
- [ ] Performance optimization
- [ ] Accessibility audit
- [ ] Cross-browser testing
- [ ] Production build
- [ ] Deploy to hosting
- [ ] Verify live site

**Notes:**
- [Add notes as you progress]

---

## Key Metrics

| Metric | Target | Current |
|--------|--------|---------|
| Lighthouse Score | 90+ | - |
| Core Web Vitals | All Green | - |
| Bundle Size | <100KB | - |
| WCAG 2.1 AA | ✅ Compliant | - |
| Mobile Ready | ✅ Yes | - |

---

## Blockers & Issues

| Issue | Status | Resolution |
|-------|--------|-----------|
| [Add if any] | | |

---

## Team Notes

- [Add team communication, decisions, feedback]
- [Track changes and iterations]

---

## Launch Checklist

- [ ] All phases complete
- [ ] Testing passed
- [ ] Performance verified
- [ ] Accessibility audit passed
- [ ] Domain configured
- [ ] Deployment tested
- [ ] Analytics configured
- [ ] Monitoring active
- [ ] Team ready
- [ ] Launch! 🚀
```

**Style:**
- Real-time progress tracking
- Visual status indicators
- Metrics dashboard
- Blocker logging
- Milestone tracking

---

## Step 8: Update CSS Theme

**File:** `src/styles/globals.css`

**Action:** Replace colors in `@theme` block:

```css
@theme {
  --color-primary: {{color_primary}};
  --color-secondary: {{color_secondary}};
  --color-accent: {{color_accent}};
  --color-neutral: {{color_neutral}};
}
```

---

## Step 9: Create Legal Pages (if requested)

**If `include_privacy === true`:**

Create `src/pages/privacy.astro` following:
- Industry-standard privacy policy structure
- Cover: data collection, usage, retention, user rights
- GDPR/CCPA compliant language
- Clear, accessible writing
- Link to contact for privacy questions

**If `include_terms === true`:**

Create `src/pages/terms.astro` following:
- Industry-standard terms structure
- Cover: user obligations, liability, dispute resolution
- Intellectual property rights
- Service limitations
- Modification/termination clauses

---

## Step 10: Ensure SEO Compliance

**All generated files must be SEO-friendly.**

### Meta Tags (in Layout.astro & Page-specific)

**Required in `src/layouts/Layout.astro`:**
```html
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<meta name="theme-color" content="{{color_primary}}" />
<meta name="description" content="{{product_description}}" />
<meta name="robots" content="index, follow" />
<meta name="author" content="{{product_name}}" />
```

**Required per page (index.astro, privacy.astro, terms.astro):**
```html
<meta property="og:title" content="{{page_title}}" />
<meta property="og:description" content="{{page_description}}" />
<meta property="og:type" content="website" />
<meta property="og:url" content="https://{{domain}}/{{page_path}}" />
<meta name="twitter:card" content="summary_large_image" />
<meta name="twitter:title" content="{{page_title}}" />
<meta name="twitter:description" content="{{page_description}}" />
```

### Semantic HTML

**Requirements:**
- `<h1>` once per page (main headline)
- `<h2>`, `<h3>` for hierarchy (in order)
- `<nav>` for navigation
- `<main>` for primary content
- `<footer>` for footer
- `<article>` for blog/content sections
- `<section>` for content groups

### Image Optimization

**All images must have:**
- `alt` text (descriptive, includes keywords)
- `width` and `height` attributes
- WebP format (with fallback to PNG/JPG)
- Compressed (< 100KB per image)

**Example:**
```html
<img 
  src="/assets/uploads/product.webp" 
  alt="{{product_name}} dashboard interface showing {{feature}}"
  width="1200"
  height="600"
  loading="lazy"
/>
```

### Structured Data (Schema.org)

**Add JSON-LD to index.astro:**
```json
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "{{product_name}}",
  "description": "{{product_description}}",
  "brand": {
    "@type": "Brand",
    "name": "{{product_name}}"
  },
  "offers": {
    "@type": "Offer",
    "availability": "https://schema.org/InStock",
    "priceCurrency": "USD",
    "price": "TBD"
  }
}
```

### Page Titles & Descriptions

**Format (best practice):**
- Title: `{{Product Name}} | {{Unique Value Prop}}` (max 60 chars)
- Description: `{{Benefit-focused summary}} | {{CTA}}` (max 160 chars)

**Examples:**
- ❌ "Welcome to {{product_name}}"
- ✅ "{{product_name}} | {{Value Prop}} - Save {{time/money}}"

### Sitemap & Robots

**Create `public/sitemap.xml`:**
```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://{{domain}}/</loc>
    <priority>1.0</priority>
  </url>
  <url>
    <loc>https://{{domain}}/privacy</loc>
    <priority>0.3</priority>
  </url>
  <url>
    <loc>https://{{domain}}/terms</loc>
    <priority>0.3</priority>
  </url>
</urlset>
```

**Create `public/robots.txt`:**
```
User-agent: *
Allow: /
Sitemap: https://{{domain}}/sitemap.xml
```

### Performance (SEO Impact)

**Lighthouse targets:**
- Performance: 90+
- Accessibility: 90+
- Best Practices: 90+
- SEO: 100

**Core Web Vitals:**
- LCP (Largest Contentful Paint): < 2.5s
- FID (First Input Delay): < 100ms
- CLS (Cumulative Layout Shift): < 0.1

### Accessibility (WCAG 2.1 AA)

**Required:**
- Color contrast: 4.5:1 minimum (text)
- Keyboard navigation: Tab through all interactive elements
- Alt text: All images, icons
- ARIA labels: Form fields, buttons
- Focus indicators: Visible on all interactive elements

### Content Guidelines

**All copy must:**
- Include target keywords (naturally)
- Answer user questions in first paragraph
- Use short paragraphs (2-3 sentences max)
- Include internal links (if multi-page)
- Include clear CTA
- Be scannable (headings, bullets)

---

## Output Schema

```json
{
  "status": "success",
  "files_generated": [
    "PRD.md",
    "spec.md",
    "tasks.md",
    "progress.md",
    "src/pages/privacy.astro (if requested)",
    "src/pages/terms.astro (if requested)"
  ],
  "files_updated": [
    "src/styles/globals.css"
  ],
  "folders_created": [
    "public/assets/uploads/"
  ],
  "next_steps": [
    "Review PRD.md for product direction",
    "Review spec.md for technical requirements",
    "Follow phases in tasks.md",
    "Track progress in progress.md",
    "npm install && npm run dev",
    "Start Phase 1: Design & Planning"
  ]
}
```

---

## Quality Standards

All generated documents should follow:

✅ **PRD.md**
- Executive-level clarity
- Specific, measurable objectives
- Competitive analysis included
- Success metrics defined

✅ **spec.md**
- Technical accuracy
- Current industry standards
- Specific requirements (not vague)
- Performance benchmarks referenced

✅ **tasks.md**
- Actionable checkboxes
- Time estimates provided
- Clear deliverables
- QA criteria included

✅ **progress.md**
- Real-time tracking possible
- Visual status indicators
- Metrics dashboard
- Blocker documentation

---

## Error Handling

**Invalid input:**
```
❌ Color "xyz" invalid. Format: #RRGGBB
→ Ask user to provide correct hex
```

**Missing required field:**
```
❌ {{field_name}} is required
→ Ask user to provide value
```

**Generation failed:**
```
❌ Could not generate {{document}}
→ Retry or ask user to verify input
```

---

## Step 11: Deploy Configuration

**Prepare for deployment to Cloudflare Pages or GitHub Pages.**

### Cloudflare Pages

**File:** `wrangler.toml` (already created)

**Deploy:**
```bash
npm run build
wrangler pages deploy dist/
```

Or connect GitHub for auto-deploy in Cloudflare Dashboard.

### GitHub Pages

**File:** `.github/workflows/deploy.yml` (already created)

**Deploy:**
1. Push to main/master branch
2. GitHub Actions auto-builds & deploys
3. Site: `https://username.github.io/repo-name/`

**Enable in Repository:**
- Settings → Pages → Source: Deploy from a branch
- Branch: gh-pages
- Folder: / (root)

### Pre-Deployment Checklist

**Code & Build:**
- [ ] `npm run build` succeeds
- [ ] No console errors
- [ ] `dist/` folder generated
- [ ] Size < 1MB

**Performance:**
- [ ] Lighthouse 90+ (Performance, Accessibility, Best Practices)
- [ ] Lighthouse 100 (SEO)
- [ ] Core Web Vitals green

**Content:**
- [ ] All product images optimized
- [ ] Colors applied correctly
- [ ] Copy reviewed
- [ ] Links working
- [ ] Contact/CTA ready

**SEO:**
- [ ] Meta tags in place
- [ ] sitemap.xml created
- [ ] robots.txt created
- [ ] Structured data added

### Domain Configuration

**Cloudflare Pages:**
- Dashboard → Pages → Custom domain
- Point nameservers to Cloudflare
- SSL auto-enabled

**GitHub Pages:**
- Settings → Pages → Custom domain
- Add DNS A records (185.199.108.153, etc)
- Wait 24-48h for SSL cert

### Environment Variables (optional)

**Cloudflare:**
- Dashboard → Pages → Settings → Environment variables

**GitHub Pages:**
- No server-side variables (static site)
- For tracking: Google Analytics ID in HTML

### Continuous Deployment

**Cloudflare:** Auto-deploys on push to main/master
**GitHub:** GitHub Actions auto-deploys on push

Both support preview builds for pull requests.

### Documentation

See `DEPLOYMENT.md` for:
- Step-by-step setup
- Troubleshooting
- Monitoring & analytics
- Rollback procedures
- Cost comparison

---

## Writing Skills (Installed)

**Location:** `.claude/skills/`

### anti-ai-writing
**Path:** `.claude/skills/anti-ai-writing/SKILL.md`

Transform AI-assisted drafts into authentic, human-sounding content.
- SUCKS Framework (Specific, Unique, Clear, Kept Simple, Sticky)
- Eliminates AI tells and patterns
- Applied to: product description, value propositions

### hook-and-headline-writing
**Path:** `.claude/skills/hook-and-headline-writing/SKILL.md`

Create attention-grabbing headlines and hooks.
- 15 proven formulas
- 4 U's Test (Useful, Unique, Urgent, Ultra-specific)
- Applied to: headlines, taglines, CTAs

**How to use:** Call skills via `/anti-ai-writing` and `/hook-and-headline-writing` commands (Step 1.5)

---

## Notes

- All documents follow **2026 SaaS industry standards**
- Use **current best practices** for each document type
- Include **specific examples** from user input
- Make content **immediately actionable**
- Documents are **version-controllable** (commit to git)
- Designed for **both technical and non-technical stakeholders**
- **Writing skills installed:** `.claude/skills/anti-ai-writing/` and `.claude/skills/hook-and-headline-writing/`
- **Claude users:** Call skills via `/anti-ai-writing` and `/hook-and-headline-writing` in Step 1.5
- **Non-Claude agents:** Read skill documentation in `.claude/skills/` for frameworks and principles
