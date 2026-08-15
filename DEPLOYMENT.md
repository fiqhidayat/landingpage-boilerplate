# Deployment Guide

Deploy landing page to Cloudflare Pages or a Docker container.

## Option 1: Cloudflare Pages

### Prerequisites
- Cloudflare account
- Domain configured in Cloudflare (optional)
- Wrangler CLI installed: `npm install -g @cloudflare/wrangler`

### Setup

1. **Connect repository:**
```bash
wrangler pages project create landingpage-boilerplate
```

2. **Configure `wrangler.toml`:**
```toml
name = "landingpage-boilerplate"
pages_build_output_dir = "dist"

[build]
command = "npm run build"
cwd = "./"
```

3. **Deploy:**
```bash
wrangler pages deploy dist/
```

Or connect GitHub for auto-deploy:
- Go to Cloudflare Dashboard
- Pages → Create project → Connect to Git
- Select repository
- Build settings: 
  - Framework: Astro
  - Build command: `npm run build`
  - Build output directory: `dist`
- Deploy

### Environment Variables (if needed)
Set in Cloudflare Dashboard → Pages → Settings → Environment variables

---

## Option 2: Docker Container

### Prerequisites
- Docker installed
- Docker Compose (bundled with Docker Desktop)

### Build & run

```bash
docker compose up -d --build
```

Site available at `http://localhost:8080`.

### What it does
- `Dockerfile`: multi-stage build — builds the Astro static site with Node 20, then serves `dist/` via nginx
- `docker-compose.yml`: maps container port 80 → host port 8080

### Manual (without compose)
```bash
docker build -t landingpage-boilerplate .
docker run -d -p 8080:80 landingpage-boilerplate
```

### Deploy to a server/VPS
```bash
# On the server, with repo cloned:
docker compose up -d --build

# Update after a git pull:
docker compose up -d --build
```

### Deploy to a container registry (e.g. for cloud hosting)
```bash
docker build -t <registry>/<image>:latest .
docker push <registry>/<image>:latest
```

---

## Option 3: Manual Deploy

### Build locally:
```bash
npm run build
```

Output in `dist/` folder.

### Deploy `dist/` to any static host:
- Vercel
- Netlify
- AWS S3 + CloudFront
- Any FTP/SFTP hosting

---

## Pre-Deployment Checklist

### Code
- [ ] All changes committed
- [ ] Tests passing (if any)
- [ ] No console errors/warnings
- [ ] SEO meta tags in place
- [ ] Images optimized

### Build
- [ ] `npm run build` succeeds
- [ ] No build warnings
- [ ] `dist/` folder generated
- [ ] Size reasonable (< 1MB for simple page)

### Performance
- [ ] Run Lighthouse audit
- [ ] Performance: 90+
- [ ] Accessibility: 90+
- [ ] SEO: 100
- [ ] Best Practices: 90+

### Content
- [ ] Product name correct
- [ ] All product images uploaded
- [ ] Color scheme applied
- [ ] Copy reviewed
- [ ] Links working
- [ ] Contact form/CTA ready

### Analytics (optional)
- [ ] Google Analytics code added
- [ ] Facebook Pixel (if e-commerce)
- [ ] Track conversions

---

## Domain Configuration

### Cloudflare Pages
1. Dashboard → Pages → Select project
2. Custom domain → Add domain
3. Point nameservers to Cloudflare
4. SSL auto-enabled

### Docker Container
1. Point domain's A record to the server's IP
2. Put nginx/Caddy/Traefik in front as a reverse proxy for TLS termination
3. Or use Cloudflare as a proxy in front of the container for free SSL

---

## Continuous Deployment

### Cloudflare Pages
- Auto-deploys on push to main/master
- Preview builds for pull requests
- Rollback available in dashboard

### Docker Container
- No built-in CI/CD — rebuild and redeploy manually, or wire up your own pipeline (GitHub Actions, GitLab CI, etc.) to build the image and `docker compose up -d --build` on the server

---

## Troubleshooting

### Build fails
```bash
npm run build
# Check errors, fix, then push
```

### Site not updating
- Clear browser cache (Ctrl+Shift+Del)
- Docker: confirm the image was rebuilt (`docker compose up -d --build`)
- Cloudflare Pages: Check Actions tab

### 404 errors on routes
- Astro generates static HTML
- Routes map to files: `/about` → `about/index.html`
- Check `dist/` folder structure

### Slow performance
- Optimize images to WebP
- Lazy load images: `loading="lazy"`
- Enable Cloudflare compression
- Test: PageSpeed Insights, Lighthouse

---

## Rollback

### Cloudflare Pages
1. Dashboard → Pages → Deployments
2. Click past version
3. Click "Rollback"

### Docker Container
1. Re-tag and redeploy a previous image version, or
2. `git checkout` a previous commit and rebuild: `docker compose up -d --build`

---

## Monitoring

### Cloudflare Analytics
- Dashboard → Analytics
- Traffic, errors, performance

### Docker Container
- No built-in analytics
- Add Google Analytics/Plausible
- Container health: `docker compose logs -f` or `docker stats`

### Uptime Monitoring
- UptimeRobot (free)
- StatusPage.io
- Cloudflare monitoring

---

## SSL/TLS Certificate

### Cloudflare Pages
- Auto-enabled, auto-renews
- HTTPS on all requests

### Docker Container
- No built-in TLS — terminate SSL with a reverse proxy (Caddy, nginx + Let's Encrypt/Certbot, Traefik) or put Cloudflare in front of the container

---

## Cost

### Cloudflare Pages
- **Free:** Unlimited sites, builds, bandwidth
- **Pro:** $20/month (custom features)

### Docker Container
- Cost of the host/VPS running Docker (varies by provider)
- No platform fee — you own the infrastructure

### Custom Domain
- ~$10-15/year (domain registrar)
