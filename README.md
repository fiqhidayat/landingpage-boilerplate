# Landing Page Boilerplate

A starter project for building landing pages with Astro and Tailwind CSS. Instead of writing everything by hand, you talk to an AI agent (Claude or another one), answer a few questions about your product, and it writes the project docs and sets up your brand colors for you.

You don't need to know Astro or Tailwind going in — this README walks you through it.

## What is this, exactly?

Three things working together:

- **Astro** — builds your site as fast, static HTML. No heavy JavaScript framework, just plain pages that load quickly.
- **Tailwind CSS** — lets you style things with utility classes (`bg-primary`, `text-lg`, etc.) instead of writing custom CSS files.
- **An AI skill** — a set of instructions living in this repo that tells your AI agent how to interview you about your product and generate the planning docs (`PRD.md`, `spec.md`, `tasks.md`, `progress.md`).

You still write the actual page code yourself (or with the AI's help) — the skill's job is to get you from "blank repo" to "clear plan and correct brand colors," not to write your whole site for you.

## Before you start

You'll need:

- A [GitHub](https://github.com) account — you'll fork this repo to your own account before doing anything else
- A [Cloudflare](https://dash.cloudflare.com/sign-up) account — free tier is fine, needed later for deploying the site
- [Node.js](https://nodejs.org) installed (v18 or newer)
- Git
- An AI coding agent — Claude Code is the easiest path here, but the instructions also work with ChatGPT, other Claude apps, or anything that can read a markdown file and follow it

## Step 1: Get the project on your machine

Fork this repo to your own GitHub account first — click **Fork** at the top of the repo page on GitHub. You need your own copy so you can push changes and connect it to Cloudflare later.

Then clone your fork:

```bash
git clone <your-fork-url>
cd landing-page-boilerplate
npm install
```

`npm install` downloads everything the project depends on. This can take a minute the first time.

## Step 2: Run the generator

This is the main event. You're going to answer some questions about your product, and the AI will turn your answers into planning documents.

**If you're using Claude Code**, just type:

```
/generate-landing-page
```

If the slash command doesn't work for some reason, you can trigger it manually by telling Claude:

```
Execute the skill in .claude/skills/generate-landing-page/SKILL.md
```

**If you're using a different AI agent** (ChatGPT, another Claude app, etc.), tell it:

```
Execute the skill in .agents/skills/generate-landing-page/SKILL.md
```

### What happens when you run it

The AI will ask you about 14 things — your product name, a short description, your target audience, three value propositions, four brand colors, some design references you like, and whether you need Privacy/Terms pages. It checks your answers make sense (hex colors need to look like `#3b82f6`, links need to be real URLs) and asks again if something's off.

Once it has everything, it generates:

1. **PRD.md** — what you're building and why, written like a real product doc
2. **spec.md** — the technical plan (components, layout, integrations)
3. **tasks.md** — a checklist broken into 5 phases, so you know what to do next
4. **progress.md** — a tracker you update as you go
5. Privacy/Terms pages, if you asked for them
6. Your brand colors, wired into `src/styles/globals.css`

At the end, you have a real plan sitting in your project folder instead of a blank page and a blinking cursor.

## Step 3: Start developing

```bash
npm run dev
```

Opens the site at `http://localhost:4321`. Every time you save a file, the page updates automatically.

From here, open `tasks.md` and work through the phases in order:

1. **Design & Planning** — settle on the look, using the docs you just generated
2. **Component Development** — build out the pieces (Hero, Features, Footer, etc.) already stubbed out in `src/components/`
3. **Page Assembly** — put the pieces together in `src/pages/index.astro`
4. **Content & Copy** — write the real headlines and body text
5. **Polish & Deploy** — performance and accessibility checks, then ship it

Check things off in `progress.md` as you go, so you (or anyone else picking this up) can see where things stand.

## Adding your own images and logo

Drop your files into `public/assets/uploads/`:

```
public/assets/uploads/
├── logo.svg
├── hero-image.png
└── product-screenshot.png
```

Then reference them in a component like a normal `<img>` tag:

```astro
<img src="/assets/uploads/hero-image.png" alt="Hero" />
```

## Changing brand colors later

Tailwind v4 doesn't use a `tailwind.config.js` file — colors live directly in `src/styles/globals.css` under `@theme`. Edit them any time:

```css
@theme {
  --color-primary: #3b82f6;
  --color-secondary: #1e40af;
  --color-accent: #f59e0b;
  --color-neutral: #f3f4f6;
}
```

Everywhere you used `bg-primary`, `text-accent`, etc. in your components will update automatically.

## Adding a custom font

Add a link tag in `src/layouts/Layout.astro`:

```html
<link href="https://fonts.googleapis.com/css2?family=YourFont:wght@400;700&display=swap" rel="stylesheet">
```

## Project layout

```
.
├── .claude/
│   ├── commands.json           # defines the /generate-landing-page command
│   └── skills/
│       └── generate-landing-page/SKILL.md   # instructions Claude follows
├── .agents/
│   └── skills/
│       └── generate-landing-page/SKILL.md   # same thing, for other AI agents
├── src/
│   ├── components/             # Hero, Features, Footer, etc.
│   ├── layouts/                # shared page layout
│   ├── pages/                  # your actual pages (index.astro, privacy.astro...)
│   └── styles/                 # globals.css — brand colors live here
├── public/assets/uploads/      # your images go here
├── Dockerfile                  # for self-hosting with Docker
├── docker-compose.yml
├── wrangler.toml               # for deploying to Cloudflare Pages
├── PRD.md, spec.md, tasks.md, progress.md   # generated once you run the skill
└── DEPLOYMENT.md                # full deploy instructions
```

## Deploying your site

Once you're happy with it, you have two easy options:

**Cloudflare Pages:**
```bash
npm run build
wrangler pages deploy dist/
```
Or just connect your GitHub repo in the Cloudflare dashboard and it'll redeploy every time you push.

**Docker (self-hosted):**
```bash
docker compose up -d --build
```
This builds the site and serves it with nginx at `http://localhost:8080`.

Full walkthrough with troubleshooting is in `DEPLOYMENT.md`.

## Things worth knowing

- **Performance target:** Lighthouse score 90+ across the board, bundle under 100KB gzipped.
- **Accessibility:** components are built to meet WCAG 2.1 AA — keyboard-navigable, sufficient color contrast, alt text on images.

## When something breaks

**The skill doesn't seem to run.** Make sure your AI agent can actually read files from `.claude/skills/` (or `.agents/skills/`) and write to your project root — some sandboxed or restricted agents block file writes by default.

**Images aren't showing up.** Double check the file is actually in `public/assets/uploads/` and that you're referencing it as `/assets/uploads/filename`, not the full local path.

**Build is failing.** Nine times out of ten, a clean reinstall fixes it:
```bash
rm -rf node_modules package-lock.json
npm install
npm run build
```

## Useful docs

- [Astro Docs](https://docs.astro.build)
- [Tailwind CSS Docs](https://tailwindcss.com/docs)
- [Claude Code Docs](https://github.com/anthropics/claude-code)

## License

MIT

---

Made by Taufik Hidayat
